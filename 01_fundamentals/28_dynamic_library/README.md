# Dynamic Libraries in C

In this section, you will learn about dynamic libraries in C, their creation, usage, and advantages.

## What is a Dynamic Library?
- A dynamic library is a collection of object files that are loaded into memory at runtime.
- The code from the library is not part of the executable, resulting in a smaller file size and the ability to update the library without recompiling the program.
- Dynamic libraries typically have the `.so` extension on Linux and `.dll` on Windows.

## Creating a Dynamic Library

1. **Write the Source Files**:
   - Create one or more `.c` files containing the functions you want to include in the library.

   Example:
   ```c
   // math_functions.c
   int add(int a, int b) {
       return a + b;
   }

   int subtract(int a, int b) {
       return a - b;
   }
   ```

2. **Compile the Source Files**:
   - Use `gcc` to compile the source files into position-independent code (PIC).
   ```bash
   gcc -c -fPIC math_functions.c
   ```

3. **Create the Dynamic Library**:
   - Use `gcc` to create the shared library.
   ```bash
   gcc -shared -o libmath.so math_functions.o
   ```

4. **Link the Dynamic Library**:
   - Use `gcc` to link the library with your program.
   ```bash
   gcc -o program main.c -L. -lmath
   ```

   - `-L.` specifies the directory containing the library.
   - `-lmath` links the `libmath.so` library.

5. **Set the Library Path**:
   - Use the `LD_LIBRARY_PATH` environment variable to specify the library path.
   ```bash
   export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH
   ```

## Example: Using a Dynamic Library

### Source File: `main.c`
```c
#include <stdio.h>

int add(int a, int b);
int subtract(int a, int b);

int main() {
    printf("Addition: %d\n", add(5, 3));
    printf("Subtraction: %d\n", subtract(5, 3));
    return 0;
}
```

### Commands
```bash
gcc -c -fPIC math_functions.c
gcc -shared -o libmath.so math_functions.o
gcc -o program main.c -L. -lmath
export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH
./program
```

## Advantages of Dynamic Libraries
- Smaller executable size.
- Libraries can be updated without recompiling the program.
- Shared among multiple programs, reducing memory usage.

## Disadvantages of Dynamic Libraries
- Slightly slower execution due to runtime linking.
- Requires the library to be present at runtime.

## Summary
Dynamic libraries are a flexible way to reuse code in C programs. Understanding how to create and use them is essential for efficient software development.