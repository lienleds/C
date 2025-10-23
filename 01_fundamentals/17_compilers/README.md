# Cross Compiler and Native Compiler

In this section, you will learn about cross compilers and native compilers in C.

## Topics

- What is a Compiler?
- Native Compiler
- Cross Compiler
- Differences and Use Cases
- Tips for Checking Libraries with a Compiler

## What is a Compiler?

A compiler is a program that translates source code written in a high-level language (like C) into machine code that can be executed by a computer.

## Native Compiler

- A native compiler generates machine code for the same platform on which it is running.
- Example: GCC running on a Linux machine to compile code for the same Linux machine.

### Example
```bash
gcc -o program program.c
./program
```

## Cross Compiler

- A cross compiler generates machine code for a platform different from the one on which it is running.
- Used for embedded systems and cross-platform development.
- Example: Compiling code on a Linux machine for an ARM-based microcontroller.

### Example
```bash
arm-none-eabi-gcc -o program program.c
```

## Differences Between Native and Cross Compilers

| Feature            | Native Compiler               | Cross Compiler               |
|--------------------|-------------------------------|------------------------------|
| Target Platform    | Same as host platform         | Different from host platform |
| Use Case           | General-purpose development   | Embedded systems, IoT        |
| Example Tools      | GCC, Clang                   | arm-none-eabi-gcc, MinGW     |

## Tips for Checking Libraries with a Compiler

1. **Check for Installed Libraries**
   - Use the `ldconfig` command to list installed libraries (Linux):
     ```bash
     ldconfig -p | grep <library_name>
     ```

2. **Verify Library Linking**
   - Use the `-l` flag with `gcc` to link a specific library:
     ```bash
     gcc -o program program.c -l<library_name>
     ```

3. **Check Library Paths**
   - Use the `-L` flag to specify custom library paths:
     ```bash
     gcc -o program program.c -L<path_to_library> -l<library_name>
     ```

4. **Debug Linking Issues**
   - Use the `ldd` command to check shared library dependencies:
     ```bash
     ldd ./program
     ```

5. **Static vs Dynamic Linking**
   - Use the `-static` flag for static linking:
     ```bash
     gcc -o program program.c -static -l<library_name>
     ```

## Exercise

1. Install a native compiler (e.g., GCC) and compile a simple C program.
2. Install a cross compiler (e.g., arm-none-eabi-gcc) and compile a program for a different platform.
3. Discuss scenarios where cross compilers are essential (e.g., embedded systems, cross-platform development).
4. Experiment with linking libraries using the tips provided above.