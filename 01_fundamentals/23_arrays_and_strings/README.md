# Arrays and Strings

In this section, you will learn about arrays and strings in C.

## Topics

- Declaring and Initializing Arrays
- Multi-dimensional Arrays
- String Manipulation

## Example

```c
#include <stdio.h>

int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }

    char name[] = "John";
    printf("\nName: %s\n", name);

    return 0;
}
```

## Exercise

1. Write a program to reverse an array.
2. Implement a program to count vowels in a string.
3. Create a program to sort an array of integers.