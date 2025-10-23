# Const Pointer vs Pointer to Const in C

In this section, you will learn the differences between a constant pointer and a pointer to a constant in C.

## Const Pointer (`int *const ptr`)
- A const pointer is a pointer that cannot point to another memory location after initialization.
- The value at the memory location can be modified.
- Syntax:
  ```c
  int a = 10;
  int b = 20;
  int *const ptr = &a; // Const pointer to int

  *ptr = 15; // Allowed
  ptr = &b;  // Not allowed
  ```

## Pointer to Const (`const int *ptr`)
- A pointer to a const is a pointer that cannot modify the value at the memory location it points to.
- The pointer itself can point to another memory location.
- Syntax:
  ```c
  int a = 10;
  int b = 20;
  const int *ptr = &a; // Pointer to const int

  *ptr = 15; // Not allowed
  ptr = &b;  // Allowed
  ```

## Const Pointer to Const (`const int *const ptr`)
- A const pointer to a const is a pointer that cannot modify the value at the memory location it points to, nor can it point to another memory location.
- Syntax:
  ```c
  int a = 10;
  const int *const ptr = &a; // Const pointer to const int

  *ptr = 15; // Not allowed
  ptr = &b;  // Not allowed
  ```

## Key Differences

| Feature              | Const Pointer (`int *const ptr`) | Pointer to Const (`const int *ptr`) | Const Pointer to Const (`const int *const ptr`) |
|----------------------|----------------------------------|-------------------------------------|-----------------------------------------------|
| Reassignment         | Not allowed                     | Allowed                             | Not allowed                                   |
| Value Modification   | Allowed                         | Not allowed                         | Not allowed                                   |

## Example: Const Pointer

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 20;
    int *const ptr = &a;

    *ptr = 15; // Allowed
    // ptr = &b; // Not allowed

    printf("Value of a: %d\n", *ptr);

    return 0;
}
```

## Example: Pointer to Const

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 20;
    const int *ptr = &a;

    // *ptr = 15; // Not allowed
    ptr = &b; // Allowed

    printf("Value of b: %d\n", *ptr);

    return 0;
}
```

## Example: Const Pointer to Const

```c
#include <stdio.h>

int main() {
    int a = 10;
    const int *const ptr = &a;

    // *ptr = 15; // Not allowed
    // ptr = &b;  // Not allowed

    printf("Value of a: %d\n", *ptr);

    return 0;
}
```

## Summary
- **Const Pointer**: Pointer cannot be reassigned, but the value can be modified.
- **Pointer to Const**: Value cannot be modified, but the pointer can be reassigned.
- **Const Pointer to Const**: Neither the value nor the pointer can be modified.