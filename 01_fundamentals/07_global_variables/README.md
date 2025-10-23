# Global Variables

In this section, you will learn about global variables in C.

## Topics

- Declaring Global Variables
- Scope and Lifetime
- Best Practices

## Example

```c
#include <stdio.h>

int globalVar = 10; // Global variable

void display() {
    printf("Global Variable: %d\n", globalVar);
}

int main() {
    printf("Global Variable in main: %d\n", globalVar);
    display();
    return 0;
}
```

## Exercise

1. Declare a global variable and use it in multiple functions.
2. Experiment with modifying the global variable in different functions.
3. Discuss the pros and cons of using global variables.