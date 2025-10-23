# Bitwise Operations in C

Bitwise operations are used to manipulate data at the bit level. They are essential for low-level programming, such as writing device drivers, cryptography, and optimizing performance-critical code.

## Bitwise Operators

| Operator | Description                          | Example       |
|----------|--------------------------------------|---------------|
| `&`      | Bitwise AND                          | `a & b`       |
| `|`      | Bitwise OR                           | `a | b`       |
| `^`      | Bitwise XOR (exclusive OR)           | `a ^ b`       |
| `~`      | Bitwise NOT (one's complement)       | `~a`          |
| `<<`     | Left shift                           | `a << 2`      |
| `>>`     | Right shift                          | `a >> 2`      |

## Examples

### 1. Bitwise AND
```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 in binary
    int b = 3; // 0011 in binary
    int result = a & b; // 0001 in binary
    printf("Bitwise AND: %d\n", result);
    return 0;
}
```

### 2. Bitwise OR
```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 in binary
    int b = 3; // 0011 in binary
    int result = a | b; // 0111 in binary
    printf("Bitwise OR: %d\n", result);
    return 0;
}
```

### 3. Bitwise XOR
```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 in binary
    int b = 3; // 0011 in binary
    int result = a ^ b; // 0110 in binary
    printf("Bitwise XOR: %d\n", result);
    return 0;
}
```

### 4. Bitwise NOT
```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 in binary
    int result = ~a; // 1010 in binary (two's complement)
    printf("Bitwise NOT: %d\n", result);
    return 0;
}
```

### 5. Left Shift
```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 in binary
    int result = a << 1; // 1010 in binary
    printf("Left Shift: %d\n", result);
    return 0;
}
```

### 6. Right Shift
```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 in binary
    int result = a >> 1; // 0010 in binary
    printf("Right Shift: %d\n", result);
    return 0;
}
```

## Use Cases

1. **Setting a Bit**:
   - Use the OR operator to set a specific bit.
   ```c
   int setBit(int num, int pos) {
       return num | (1 << pos);
   }
   ```

2. **Clearing a Bit**:
   - Use the AND operator with the NOT operator to clear a specific bit.
   ```c
   int clearBit(int num, int pos) {
       return num & ~(1 << pos);
   }
   ```

3. **Toggling a Bit**:
   - Use the XOR operator to toggle a specific bit.
   ```c
   int toggleBit(int num, int pos) {
       return num ^ (1 << pos);
   }
   ```

4. **Checking a Bit**:
   - Use the AND operator to check if a specific bit is set.
   ```c
   int checkBit(int num, int pos) {
       return (num & (1 << pos)) != 0;
   }
   ```

## Exercises

1. Write a program to count the number of set bits in an integer.
2. Implement a function to reverse the bits of an integer.
3. Create a program to swap two numbers using bitwise XOR.
4. Explore the effect of left and right shifts on signed and unsigned integers.

## Additional Resources

- [Bitwise Operations in C](https://en.wikipedia.org/wiki/Bitwise_operation)
- [GeeksforGeeks: Bitwise Operators](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)
- [C Programming: Bit Manipulation](https://www.tutorialspoint.com/cprogramming/c_bitwise_operators.htm)