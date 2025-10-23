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