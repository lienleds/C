# Static Libraries in C

In this section, you will learn about static libraries in C, their creation, usage, and advantages.

## What is a Static Library?
- A static library is a collection of object files that are linked into a program at compile time.
- The code from the library becomes part of the executable, resulting in a larger file size but no runtime dependency on the library.
- Static libraries typically have the `.a` extension on Linux and `.lib` on Windows.

## Creating a Static Library

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
   - Use `gcc` to compile the source files into object files.
   ```bash
   gcc -c math_functions.c
   ```

3. **Create the Static Library**:
   - Use the `ar` command to create the library archive.
   ```bash
   ar rcs libmath.a math_functions.o
   ```

4. **Link the Static Library**:
   - Use `gcc` to link the library with your program.
   ```bash
   gcc -o program main.c -L. -lmath
   ```

   - `-L.` specifies the directory containing the library.
   - `-lmath` links the `libmath.a` library.

## Example: Using a Static Library

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
gcc -c math_functions.c
ar rcs libmath.a math_functions.o
gcc -o program main.c -L. -lmath
./program
```

## Advantages of Static Libraries
- Faster execution since all code is part of the executable.
- No runtime dependency on external libraries.
- Easier to distribute a single executable file.

## Disadvantages of Static Libraries
- Larger executable size.
- Updating the library requires recompiling the program.

## Summary
Static libraries are a powerful way to reuse code in C programs. Understanding how to create and use them is essential for efficient software development.