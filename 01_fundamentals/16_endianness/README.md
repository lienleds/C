# Big Endian and Little Endian

In this section, you will learn about endianness in C.

## Topics

- What is Endianness?
- Big Endian vs Little Endian
- Checking Endianness in C

## What is Endianness?

Endianness refers to the order in which bytes are stored in memory:
- **Big Endian**: The most significant byte (MSB) is stored at the smallest memory address.
- **Little Endian**: The least significant byte (LSB) is stored at the smallest memory address.

## Example: Checking Endianness

```c
#include <stdio.h>

void checkEndianness() {
    unsigned int x = 1;
    char *c = (char *)&x;

    if (*c) {
        printf("System is Little Endian\n");
    } else {
        printf("System is Big Endian\n");
    }
}

int main() {
    checkEndianness();
    return 0;
}
```

## Explanation

- The `checkEndianness` function uses a union of an integer and a character pointer to determine the byte order.
- If the first byte is the least significant byte, the system is little endian.
- If the first byte is the most significant byte, the system is big endian.

## Exercise

1. Write a program to convert a number from little endian to big endian.
2. Experiment with different data types to observe their memory layout.
3. Discuss scenarios where understanding endianness is important (e.g., network protocols, file formats).