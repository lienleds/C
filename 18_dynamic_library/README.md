# Dynamic Libraries in C

Dynamic libraries (shared libraries: `.so` on Linux, `.dll` on Windows, `.dylib` on macOS) are compiled code modules loaded and linked into programs at runtime. They enable code reuse, modularity, and efficient memory usage.

---

## Table of Contents

- [Features](#features)
- [Creating a Dynamic Library](#creating-a-dynamic-library)
- [Using a Dynamic Library](#using-a-dynamic-library)
- [Advantages & Disadvantages](#advantages--disadvantages)
- [Practical Example](#practical-example)
- [Position Independent Code (`-fPIC`)](#position-independent-code--fpic-)
- [Advanced Concepts](#advanced-concepts)
- [Additional Resources](#additional-resources)

---

## Features

- **Shared Code:** Multiple programs use the same library code.
- **Runtime Linking:** Libraries are loaded when the program runs.
- **Reduced Memory Usage:** Only one copy of the library is loaded.
- **Easy Updates:** Update the library without recompiling dependent programs.

---

## Creating a Dynamic Library

### 1. Write the Library Code

```c
// mylib.c
#include <stdio.h>
void hello() {
  printf("Hello from dynamic library!\n");
}
```

### 2. Compile as a Shared Library

#### What is `-fPIC`?

- `-fPIC` stands for "Position Independent Code".
- Generates code that can be loaded at any memory address (required for shared libraries).

#### Compile Command

```bash
gcc -fPIC -shared -o libmylib.so mylib.c
```

- `-fPIC`: Generates position-independent code.
- `-shared`: Produces a shared library (`.so` file).
- `-o libmylib.so`: Output file name.

---

## Using a Dynamic Library

### Link at Compile Time

```bash
gcc -o main main.c -L. -lmylib
export LD_LIBRARY_PATH=.
./main
```

- `-L.`: Linker searches current directory for libraries.
- `-lmylib`: Links against `libmylib.so` (prefix `lib` and suffix `.so` are implied).

### Load at Runtime

```c
#include <dlfcn.h>
void *handle = dlopen("./libmylib.so", RTLD_LAZY);
void (*hello)() = dlsym(handle, "hello");
hello();
dlclose(handle);
```

- `dlopen`: Loads the shared library at runtime.
- `dlsym`: Gets the address of the `hello` function.
- `dlclose`: Unloads the library.

---

## Advantages & Disadvantages

### Advantages

- Saves disk and memory space.
- Easier maintenance and updates.
- Modular program design.

### Disadvantages

- Dependency/version management can be complex.
- Possible runtime errors if libraries are missing.
- Slightly slower startup due to runtime linking.

---

## Practical Example

**main.c**

```c
#include <stdio.h>
void hello();
int main() {
  hello();
  return 0;
}
```

**Build and Run**

```bash
gcc -o main main.c -L. -lmylib
export LD_LIBRARY_PATH=.
./main
```

---

## Position Independent Code (`-fPIC`)

When compiling a shared library, code must run at any memory address. The `-fPIC` flag tells the compiler to generate "position independent code" so the library can be loaded anywhere in memory.

### Why is PIC Needed?

- **Without PIC:** Code expects a fixed address; may crash if loaded elsewhere.
- **With PIC:** Uses relative addressing; works at any address.

#### Diagram: How PIC Works

```
+-------------------+      +-------------------+
| Program A         |      | Program B         |
|                   |      |                   |
| Loads libmylib.so |      | Loads libmylib.so |
| at 0x400000       |      | at 0x600000       |
+-------------------+      +-------------------+

libmylib.so compiled with -fPIC:
- Can run at 0x400000 (Program A)
- Can run at 0x600000 (Program B)
- No code changes needed!
```

#### How PIC is Implemented

- Uses relative addressing for data and function calls.
- Avoids hardcoded absolute addresses.
- The dynamic linker can relocate the library as needed.

#### Summary Table

| Flag   | Use Case                | Result                        |
|--------|-------------------------|-------------------------------|
| -fPIC  | Shared libraries (.so)  | Position independent code     |
| (none) | Static binaries (.exe)  | Fixed address code            |

---

## Advanced Concepts

### 1. Versioning and SONAME

- **SONAME** specifies the library version for the dynamic linker.
- Ensures compatibility between different library versions.
- Example:
  ```bash
  gcc -shared -Wl,-soname,libmylib.so.1 -o libmylib.so.1.0 mylib.c
  ```

### 2. Symbol Visibility

- By default, all global symbols are exported.
- Use `__attribute__((visibility("default")))` to export, or `static` to hide symbols.
- Reducing exported symbols improves security and performance.
  ```c
  __attribute__((visibility("hidden"))) void internal_function() { ... }
  ```

### 3. ABI Compatibility

- ABI (Application Binary Interface) stability is crucial.
- Changing function signatures or data structures can break compatibility.
- Best practice: Use opaque pointers and avoid changing public interfaces.

### 4. Using `ldconfig` and Library Paths

- Install shared libraries system-wide (e.g., `/usr/lib`).
- Run `sudo ldconfig` to update the linker cache.
- Use `/etc/ld.so.conf` for custom library paths.
- `LD_LIBRARY_PATH` can be used for temporary overrides.

### 5. Dynamic Loading with `dlopen`/`dlsym`

- Use `dlerror()` to check for errors.
- Useful for plugins and modular applications.
  ```c
  char *error;
  error = dlerror();
  if (error) { fprintf(stderr, "%s\n", error); }
  ```

### 6. Platform Differences

- **Linux:** `.so` files, ELF format.
- **Windows:** `.dll` files, PE format.
- **macOS:** `.dylib` files, Mach-O format.
- Linking and loading commands differ by platform.

### 7. Security Considerations

- Loading untrusted libraries can be risky.
- Use signed libraries or restrict library paths.
- Validate library sources and permissions.

### 8. Thread Safety

- Ensure shared libraries are thread-safe for multi-threaded programs.
- Use mutexes or thread-local storage as needed.

### 9. Static vs. Shared Libraries

| Type            | Linked At      | Usage                |
|-----------------|---------------|----------------------|
| Static (.a)     | Compile time  | Included in executable|
| Shared (.so)    | Runtime       | Shared among programs |

- Use static libraries for portability, shared libraries for modularity.

---
### 10. Linking a Static Library into a Dynamic Library in C

You can include object files from a static library (`.a`) when building a dynamic library (`.so`). This allows you to reuse code from a static library inside your shared library.

#### Steps

1. **Create the Static Library**
  ```bash
  gcc -c -fPIC foo.c
  ar rcs libfoo.a foo.o
  ```

2. **Link the Static Library into the Shared Library**
  ```bash
  gcc -fPIC -shared -o libbar.so bar.c -L. -lfoo
  ```
  - `-L.`: Tells the linker to look in the current directory for libraries.
  - `-lfoo`: Links against `libfoo.a`.

#### Notes

- The static library’s object code is included in the shared library.
- All code must be compiled with `-fPIC` for position independence.
- If the static library was not compiled with `-fPIC`, you may see linker warnings or errors.

#### Example

```bash
gcc -c -fPIC foo.c
ar rcs libfoo.a foo.o
gcc -fPIC -shared -o libbar.so bar.c -L. -lfoo
```
- Now, `libbar.so` contains code from both `bar.c` and `foo.c`.

#### When to Use

- When you want to distribute a shared library that includes code from a static library.
- Useful for legacy code or third-party static libraries.

#### Potential Risks

- **License Issues:** Including third-party static libraries may violate licensing terms if redistribution is restricted.
- **Symbol Conflicts:** Duplicate symbols from multiple static libraries can cause linker errors or unexpected behavior.
- **ABI Compatibility:** If the static library’s ABI changes, you must rebuild the shared library.
- **Code Bloat:** Including large static libraries can increase the size of the shared library.
- **Thread Safety:** Legacy static libraries may not be thread-safe, affecting the shared library’s reliability.
- **PIC Requirement:** All object files must be compiled with `-fPIC`; otherwise, runtime errors or crashes may occur.

#### How to Ensure All Object Files in a Static Library Use `-fPIC`

- Always compile each source file for the static library with the `-fPIC` flag:
  ```bash
  gcc -c -fPIC file1.c
  gcc -c -fPIC file2.c
  ar rcs libfoo.a file1.o file2.o
  ```
- There is no way to "fix" a static library after it is built; you must recompile all sources with `-fPIC`.
- To check if object files are compiled with `-fPIC`, use `readelf -h file.o` or `objdump -x file.o` and look for "DYN" or "REL" in the output.
- If you use third-party static libraries, verify their build flags or request a version compiled with `-fPIC`.
- Mixing non-PIC and PIC object files in a shared library can cause linker errors or unpredictable runtime behavior.
- For build systems (Makefiles, CMake), set `CFLAGS += -fPIC` globally for all sources used in static libraries intended for dynamic linking.


## Additional Resources

- [GNU Libtool Manual](https://www.gnu.org/software/libtool/manual/libtool.html)
- [Linux man page: dlopen](https://man7.org/linux/man-pages/man3/dlopen.3.html)
- [GCC Position Independent Code](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html#index-fPIC-180)