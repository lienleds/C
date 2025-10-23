# Arrays vs Pointers in C

In this section, you will learn the differences between arrays and pointers in C, including their similarities, differences, and use cases.

## What are Arrays?
- Arrays are a collection of elements of the same type stored in contiguous memory locations.
- Arrays have a fixed size defined at compile time.
- Syntax:
  ```c
  int arr[5] = {1, 2, 3, 4, 5};
  ```

## What are Pointers?
- Pointers are variables that store the memory address of another variable.
- Pointers can dynamically point to different memory locations.
- Syntax:
  ```c
  int a = 10;
  int *p = &a;
  ```

## Key Differences

| Feature              | Array                              | Pointer                            |
|----------------------|------------------------------------|------------------------------------|
| Memory Allocation    | Fixed at compile time.            | Can be dynamic (using `malloc`).  |
| Size                 | Fixed size.                       | No fixed size.                    |
| Syntax               | `arr[i]` for element access.      | `*(p + i)` for element access.    |
| Nullability          | Cannot be null.                   | Can be null.                      |
| Use Case             | Storing multiple elements.        | Dynamic memory management.        |

## Example: Array

```c
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};

    for (int i = 0; i < 5; i++) {
        printf("arr[%d] = %d\n", i, arr[i]);
    }

    return 0;
}
```

## Example: Pointer

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = (int *)malloc(5 * sizeof(int));

    for (int i = 0; i < 5; i++) {
        p[i] = i + 1;
        printf("p[%d] = %d\n", i, p[i]);
    }

    free(p);
    return 0;
}
```

## Similarities
- Both arrays and pointers can be used to access memory locations.
- The name of an array acts as a pointer to its first element.
- Pointer arithmetic can be used to traverse arrays.

## Summary
- **Arrays** are fixed in size and are ideal for storing a collection of elements.
- **Pointers** are more flexible and can dynamically allocate memory.
- Understanding the differences and similarities between arrays and pointers is crucial for effective memory management in C.