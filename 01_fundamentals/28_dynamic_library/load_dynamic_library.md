# Loading Dynamic Libraries in C

In this section, you will learn the different ways to load a dynamic library into a program during execution in C.

## Methods for Loading Dynamic Libraries

### 1. **Linking at Compile Time**
- The dynamic library is linked during the compilation of the program.
- The library must be present at runtime.
- Command:
  ```bash
  gcc -o program main.c -L. -lmath
  ```
- Example:
  ```c
  #include <stdio.h>

  int add(int a, int b);

  int main() {
      printf("Addition: %d\n", add(5, 3));
      return 0;
  }
  ```

### 2. **Loading at Runtime Using `dlopen`**
- The dynamic library is loaded explicitly at runtime using the `dlopen` function.
- Functions are accessed using `dlsym`.
- Requires `<dlfcn.h>`.

#### Example
```c
#include <stdio.h>
#include <dlfcn.h>

int main() {
    void *handle;
    int (*add)(int, int);
    char *error;

    // Load the library
    handle = dlopen("./libmath.so", RTLD_LAZY);
    if (!handle) {
        fprintf(stderr, "%s\n", dlerror());
        return 1;
    }

    // Get the symbol for the add function
    *(void **)(&add) = dlsym(handle, "add");
    if ((error = dlerror()) != NULL) {
        fprintf(stderr, "%s\n", error);
        return 1;
    }

    // Use the function
    printf("Addition: %d\n", add(5, 3));

    // Close the library
    dlclose(handle);
    return 0;
}
```

#### Commands
```bash
gcc -shared -o libmath.so math_functions.c
gcc -o program main.c -ldl
./program
```

### 3. **Using Environment Variables**
- The `LD_LIBRARY_PATH` environment variable specifies the directories to search for dynamic libraries at runtime.
- Command:
  ```bash
  export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH
  ./program
  ```

### 4. **Using `rpath`**
- The `rpath` option embeds the library path into the executable.
- Command:
  ```bash
  gcc -o program main.c -Wl,-rpath,.
  ```

### More Details: `rpath`
- **What is `rpath`?**
  - `rpath` (runtime library search path) is an embedded path in the executable that tells the dynamic linker where to look for shared libraries at runtime.
  - It is specified at compile time using the `-Wl,-rpath` linker option.

- **Advantages**:
  - Ensures the executable always finds the correct version of the library.
  - No need to set environment variables like `LD_LIBRARY_PATH`.

- **Disadvantages**:
  - Hardcodes the library path into the executable, which may reduce portability.

- **Example**:
  ```bash
  gcc -o program main.c -Wl,-rpath,/path/to/library
  ```
  - This embeds `/path/to/library` into the executable as the runtime library search path.

- **Viewing `rpath`**:
  - Use the `readelf` command to inspect the `rpath` of an executable:
    ```bash
    readelf -d program | grep rpath
    ```

### 5. **Using `ldconfig`**
- The `ldconfig` command updates the system's dynamic linker cache.
- Add the library path to `/etc/ld.so.conf` and run:
  ```bash
  sudo ldconfig
  ```

### More Details: `ldconfig`
- **What is `ldconfig`?**
  - `ldconfig` is a system utility that updates the dynamic linker cache, which is used to locate shared libraries at runtime.
  - It reads the library paths specified in `/etc/ld.so.conf` and updates the cache file `/etc/ld.so.cache`.

- **How to Use**:
  1. Add the library path to `/etc/ld.so.conf` or create a new file in `/etc/ld.so.conf.d/`.
     ```bash
     echo "/path/to/library" | sudo tee -a /etc/ld.so.conf.d/custom.conf
     ```
  2. Run `ldconfig` to update the cache:
     ```bash
     sudo ldconfig
     ```

- **Checking the Cache**:
  - Use the `ldconfig -p` command to view the current dynamic linker cache:
    ```bash
    ldconfig -p | grep <library_name>
    ```

- **Advantages**:
  - Centralized management of library paths.
  - Avoids hardcoding paths into executables.

- **Disadvantages**:
  - Requires administrative privileges to modify the cache.
  - Changes affect all programs on the system.

## Summary
- Dynamic libraries can be loaded at compile time or runtime.
- Runtime loading provides flexibility but requires careful management of library paths and symbols.
- Methods like `dlopen`, `LD_LIBRARY_PATH`, and `rpath` offer different ways to manage dynamic libraries effectively.
- Use `rpath` for embedding library paths directly into executables, ensuring portability within a specific environment.
- Use `ldconfig` for system-wide management of shared libraries, making them available to all programs without modifying individual executables.