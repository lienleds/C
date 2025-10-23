# Pointers vs References in C

In this section, you will learn the differences between pointers and references in C and C++.

## What are Pointers?
- A pointer is a variable that stores the memory address of another variable.
- Pointers are explicitly declared and manipulated.
- Syntax:
  ```c
  int a = 10;
  int *p = &a; // Pointer to variable a
  ```

## What are References?
- A reference is an alias for another variable (only available in C++).
- References are implicitly dereferenced and cannot be reassigned.
- Syntax:
  ```cpp
  int a = 10;
  int &ref = a; // Reference to variable a
  ```

## Key Differences

| Feature              | Pointer                          | Reference                        |
|----------------------|----------------------------------|----------------------------------|
| Declaration          | `int *p = &a;`                  | `int &ref = a;`                 |
| Reassignment         | Can be reassigned to point to another variable. | Cannot be reassigned after initialization. |
| Nullability          | Can be null.                    | Cannot be null.                 |
| Arithmetic           | Supports pointer arithmetic.    | Does not support arithmetic.    |
| Use Case             | Dynamic memory allocation, arrays, etc. | Parameter passing, aliases.    |

## Example: Pointer

```c
#include <stdio.h>

int main() {
    int a = 10;
    int *p = &a;

    printf("Value of a: %d\n", *p);
    *p = 20;
    printf("Updated value of a: %d\n", a);

    return 0;
}
```

## Example: Reference (C++)

```cpp
#include <iostream>

int main() {
    int a = 10;
    int &ref = a;

    std::cout << "Value of a: " << ref << std::endl;
    ref = 20;
    std::cout << "Updated value of a: " << a << std::endl;

    return 0;
}
```

## Summary
- **Pointers** are more flexible and powerful but require explicit management.
- **References** are safer and easier to use but are limited to C++.
- Understanding when to use pointers or references is crucial for efficient programming.