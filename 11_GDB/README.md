# GDB (GNU Debugger)

GDB is a powerful debugging tool for C and C++ programs. It allows you to pause program execution, inspect variables, and step through code to identify and fix issues.

## Step-by-Step Guide

### 1. Compile with Debugging Information
To use GDB, compile your program with the `-g` flag:
```bash
gcc -g -o program program.c
```

### 2. Start GDB
Run GDB with your compiled program:
```bash
gdb ./program
```

### 3. Common Commands
- **Run the program**:
  ```bash
  run
  ```
- **Set a breakpoint**:
  ```bash
  break main
  ```
- **Step through code**:
  ```bash
  step
  next
  ```
- **Inspect variables**:
  ```bash
  print variable_name
  ```
- **Continue execution**:
  ```bash
  continue
  ```
- **Quit GDB**:
  ```bash
  quit
  ```

### 4. Example Debugging Session
Given the following program:
```c
#include <stdio.h>

int main() {
    int a = 5;
    int b = 0;
    int c = a / b; // Division by zero
    printf("Result: %d\n", c);
    return 0;
}
```

Steps:
1. Compile with `-g`:
   ```bash
   gcc -g -o example example.c
   ```
2. Start GDB:
   ```bash
   gdb ./example
   ```
3. Set a breakpoint at `main`:
   ```bash
   break main
   ```
4. Run the program:
   ```bash
   run
   ```
5. Step through the code and inspect variables:
   ```bash
   step
   print a
   print b
   ```

### 5. Additional Resources
- [GDB Documentation](https://www.gnu.org/software/gdb/documentation/)
- [GDB Cheat Sheet](https://darkdust.net/files/GDB%20Cheat%20Sheet.pdf)

### Exercise
1. Debug a program with a segmentation fault and identify the faulty line.
2. Use GDB to inspect the call stack of a program with multiple functions.
3. Practice setting conditional breakpoints to pause execution only when a variable meets a specific condition.