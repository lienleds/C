# Integer Variables

In this section, you will learn about integer variables in C.

## Topics

- Declaring Integer Variables
- Signed and Unsigned Integers
- Integer Ranges

## Example

```c
#include <stdio.h>

int main() {
    int age = 25; // Signed integer
    unsigned int count = 100; // Unsigned integer

    printf("Age: %d\n", age);
    printf("Count: %u\n", count);

    return 0;
}
```

## Exercise

1. Declare signed and unsigned integers.
2. Print their values using `printf`.
3. Experiment with integer overflow.