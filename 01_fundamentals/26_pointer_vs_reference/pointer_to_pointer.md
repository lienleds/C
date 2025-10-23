# Pointer to Pointer in C

In this section, you will learn about pointers to pointers in C, their syntax, and use cases.

## What is a Pointer to Pointer?
- A pointer to a pointer is a variable that stores the address of another pointer.
- It is used to indirectly access the value of a variable through multiple levels of indirection.
- Syntax:
  ```c
  int a = 10;
  int *p = &a;   // Pointer to int
  int **pp = &p; // Pointer to pointer to int
  ```

## Key Concepts

1. **Declaration**:
   - `int **pp;` declares a pointer to a pointer to an integer.

2. **Initialization**:
   - `pp = &p;` assigns the address of pointer `p` to `pp`.

3. **Dereferencing**:
   - `*pp` gives the value of `p` (address of `a`).
   - `**pp` gives the value of `a`.

## Example: Pointer to Pointer

```c
#include <stdio.h>

int main() {
    int a = 10;
    int *p = &a;
    int **pp = &p;

    printf("Value of a: %d\n", a);
    printf("Value of a using *p: %d\n", *p);
    printf("Value of a using **pp: %d\n", **pp);

    printf("Address of a: %p\n", (void *)&a);
    printf("Address of a using p: %p\n", (void *)p);
    printf("Address of a using *pp: %p\n", (void *)*pp);

    printf("Address of p: %p\n", (void *)&p);
    printf("Address of p using pp: %p\n", (void *)pp);

    return 0;
}
```

## Use Cases

1. **Dynamic Memory Allocation**:
   - Used in multi-dimensional arrays.

2. **Function Parameters**:
   - Allows functions to modify the value of a pointer.

3. **Data Structures**:
   - Used in complex data structures like linked lists, trees, and graphs.

## Example: Modifying a Pointer in a Function

```c
#include <stdio.h>

void modifyPointer(int **pp) {
    static int b = 20;
    *pp = &b;
}

int main() {
    int a = 10;
    int *p = &a;

    printf("Before modification: %d\n", *p);
    modifyPointer(&p);
    printf("After modification: %d\n", *p);

    return 0;
}
```

## Summary
- **Pointer to Pointer** provides multiple levels of indirection.
- It is useful for dynamic memory allocation, modifying pointers in functions, and implementing complex data structures.
- Understanding pointers to pointers is essential for mastering advanced C programming concepts.