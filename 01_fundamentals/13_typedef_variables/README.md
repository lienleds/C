# Typedef Variables

In this section, you will learn about `typedef` in C.

## Topics

- Declaring Typedefs
- Use Cases
- Advantages

## Example

```c
#include <stdio.h>

typedef unsigned int uint; // Typedef for unsigned int

typedef struct {
    int id;
    char name[50];
} Student; // Typedef for struct

int main() {
    uint age = 25; // Using typedef for unsigned int
    Student s1 = {1, "John"}; // Using typedef for struct

    printf("Age: %u\n", age);
    printf("Student ID: %d, Name: %s\n", s1.id, s1.name);

    return 0;
}
```

## Explanation

- The `typedef` keyword allows you to create new names (aliases) for existing types.
- Commonly used for simplifying complex type declarations.

## Exercise

1. Create a typedef for a pointer to a function.
2. Use typedef to simplify a complex struct declaration.
3. Experiment with typedef in different scenarios.