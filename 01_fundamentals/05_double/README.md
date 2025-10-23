# Double Variables

In this section, you will learn about double variables in C.

## Topics

- Declaring Double Variables
- Precision of Doubles
- Format Specifiers

## Example

```c
#include <stdio.h>

int main() {
    double pi = 3.14159265359; // Double variable

    printf("Value of pi: %.10lf\n", pi);

    return 0;
}
```

## Exercise

1. Declare a double variable and assign a value.
2. Print the value with high precision.
3. Compare precision with float variables.