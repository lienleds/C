# Static Variables

In this section, you will learn about static variables in C.

## Topics

- Declaring Static Variables
- Scope and Lifetime
- Use Cases

## Example

```c
#include <stdio.h>

void counter() {
    static int count = 0; // Static variable
    count++;
    printf("Count: %d\n", count);
}

int main() {
    counter();
    counter();
    counter();
    return 0;
}
```

## Exercise

1. Declare a static variable inside a function and observe its behavior.
2. Compare static variables with global and local variables.
3. Discuss scenarios where static variables are useful.