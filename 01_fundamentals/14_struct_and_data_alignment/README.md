# Structs and Data Alignment

In this section, you will learn about structs and data alignment in C.

## Topics

- Declaring and Using Structs
- Nested Structs
- Data Alignment and Padding

## Example: Structs

```c
#include <stdio.h>

struct Student {
    int id;
    char name[50];
    float grade;
};

int main() {
    struct Student s1 = {1, "John", 85.5};

    printf("ID: %d\n", s1.id);
    printf("Name: %s\n", s1.name);
    printf("Grade: %.2f\n", s1.grade);

    return 0;
}
```

## Example: Data Alignment

```c
#include <stdio.h>

struct Aligned {
    char a;
    int b;
    char c;
};

int main() {
    printf("Size of struct Aligned: %lu bytes\n", sizeof(struct Aligned));

    return 0;
}
```

## Explanation

### Structs
- A `struct` is a user-defined data type that groups related variables of different types.
- Useful for representing complex data models.

### Data Alignment
- Data alignment refers to arranging data in memory to match the hardware's requirements.
- Compilers often add padding to structs to align data members to their natural boundaries.
- This can lead to unused memory (padding).

### Example of Padding
For the `struct Aligned`:
- `char a` takes 1 byte.
- `int b` takes 4 bytes but starts at a 4-byte boundary, so 3 bytes of padding are added after `a`.
- `char c` takes 1 byte, and additional padding may be added to align the struct size to a multiple of 4.

## Exercise

1. Create a struct with different data types and observe its size.
2. Experiment with reordering struct members to minimize padding.
3. Use `#pragma pack` to control padding and alignment.