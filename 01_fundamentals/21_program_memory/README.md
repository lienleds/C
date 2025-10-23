# Program Memory Layout

In this section, you will learn about the memory layout of a program and its different segments.

## Memory Segments of a Program

A program's memory is divided into the following segments:

### 1. **Text Segment**
- Contains the program's executable code (instructions).
- Read-only to prevent accidental modification.
- Example: Function definitions.

### 2. **Data Segment**
- Stores global and static variables that are initialized.
- Example:
  ```c
  int globalVar = 10; // Stored in the data segment
  ```

### 3. **BSS Segment**
- Stores global and static variables that are uninitialized or initialized to zero.
- Example:
  ```c
  static int uninitializedVar; // Stored in the BSS segment
  ```

### 4. **Heap Segment**
- Used for dynamic memory allocation.
- Grows upwards as memory is allocated.
- Example:
  ```c
  int *ptr = (int *)malloc(sizeof(int));
  ```

### 5. **Stack Segment**
- Stores local variables and function call information (e.g., return addresses).
- Grows downwards as functions are called.
- Example:
  ```c
  void func() {
      int localVar = 5; // Stored in the stack segment
  }
  ```

## Example Program

```c
#include <stdio.h>
#include <stdlib.h>

int globalVar = 10; // Data segment
static int staticVar; // BSS segment

void func() {
    int localVar = 5; // Stack segment
    int *dynamicVar = (int *)malloc(sizeof(int)); // Heap segment

    printf("Local Variable: %d\n", localVar);
    *dynamicVar = 20;
    printf("Dynamic Variable: %d\n", *dynamicVar);

    free(dynamicVar);
}

int main() {
    func();
    return 0;
}
```

## Explanation

- **Text Segment**: Contains the compiled machine code for `func` and `main`.
- **Data Segment**: Stores `globalVar`.
- **BSS Segment**: Stores `staticVar`.
- **Heap Segment**: Allocates memory dynamically using `malloc`.
- **Stack Segment**: Stores `localVar` and function call information.

## Exercise

1. Write a program that uses all memory segments (text, data, BSS, heap, stack).
2. Use `size` command to inspect the memory layout of your compiled program:
   ```bash
   gcc -o program program.c
   size program
   ```
3. Experiment with dynamic memory allocation and observe the heap's behavior.
4. Discuss scenarios where understanding memory layout is important (e.g., debugging, performance optimization).