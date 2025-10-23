# Register Variables

In this section, you will learn about register variables in C.

## Topics

- Declaring Register Variables
- Scope and Lifetime
- Use Cases

## Example

```c
#include <stdio.h>

int main() {
    register int counter = 0; // Register variable

    for (counter = 0; counter < 5; counter++) {
        printf("Counter: %d\n", counter);
    }

    return 0;
}
```

## Explanation

- The `register` keyword suggests to the compiler that the variable should be stored in a CPU register for faster access.
- The compiler may ignore this suggestion if registers are not available.
- Register variables cannot have their address taken using the `&` operator.

## Exercise

1. Declare a register variable and use it in a loop.
2. Experiment with taking the address of a register variable (observe the error).
3. Discuss scenarios where register variables might be useful.