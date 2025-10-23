# Functions

In this section, you will learn about functions in C.

## Topics

- Function Declaration and Definition
- Function Parameters
- Return Values

## Example

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3);
    printf("Sum: %d\n", result);
    return 0;
}
```

## Exercise

1. Write a function to calculate the factorial of a number.
2. Implement a function to find the maximum of two numbers.
3. Create a program with multiple functions for different tasks.

## Function Pointers

Function pointers in C allow you to store the address of a function and call it indirectly. This is useful for callbacks, dynamic function calls, and implementing polymorphism in C.

### Step-by-Step Guide

1. **Declare a Function Pointer**:
   ```c
   return_type (*pointer_name)(parameter_list);
   ```
   Example:
   ```c
   int (*operation)(int, int);
   ```

2. **Assign a Function to the Pointer**:
   ```c
   operation = &function_name;
   ```
   Example:
   ```c
   operation = &add;
   ```

3. **Call the Function Using the Pointer**:
   ```c
   result = (*operation)(arg1, arg2);
   ```
   Example:
   ```c
   int result = (*operation)(5, 3);
   ```

### Example Code

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int multiply(int a, int b) {
    return a * b;
}

int main() {
    int (*operation)(int, int);

    operation = &add;
    printf("Addition: %d\n", operation(5, 3));

    operation = &multiply;
    printf("Multiplication: %d\n", operation(5, 3));

    return 0;
}
```

### Exercise

1. Create a program that uses a function pointer to switch between different mathematical operations (e.g., add, subtract, multiply, divide).
2. Implement a callback mechanism using function pointers.