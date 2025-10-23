# Dynamic Memory Allocation: malloc, calloc, realloc

This document explains the dynamic memory allocation functions in C: `malloc`, `calloc`, and `realloc`, along with their differences.

## 1. malloc (Memory Allocation)

### What is `malloc`?
- Allocates a block of memory of the specified size (in bytes).
- Does not initialize the memory (contains garbage values).
- Returns a pointer to the beginning of the block.

### Syntax:
```c
void *malloc(size_t size);
```

### Example:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr = (int *)malloc(5 * sizeof(int)); // Allocate memory for 5 integers

    if (arr == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    for (int i = 0; i < 5; i++) {
        arr[i] = i + 1; // Assign values
        printf("%d ", arr[i]);
    }

    free(arr); // Free allocated memory
    return 0;
}
```

## 2. calloc (Contiguous Allocation)

### What is `calloc`?
- Allocates memory for an array of elements.
- Initializes all bytes to zero.
- Returns a pointer to the beginning of the block.

### Syntax:
```c
void *calloc(size_t num, size_t size);
```

### Example:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr = (int *)calloc(5, sizeof(int)); // Allocate and initialize memory for 5 integers

    if (arr == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]); // All elements are initialized to 0
    }

    free(arr); // Free allocated memory
    return 0;
}
```

## 3. realloc (Reallocation)

### What is `realloc`?
- Resizes a previously allocated memory block.
- Can increase or decrease the size of the block.
- May move the memory block to a new location if necessary.

### Syntax:
```c
void *realloc(void *ptr, size_t new_size);
```

### Example:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr = (int *)malloc(3 * sizeof(int)); // Allocate memory for 3 integers

    if (arr == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    for (int i = 0; i < 3; i++) {
        arr[i] = i + 1;
    }

    arr = (int *)realloc(arr, 5 * sizeof(int)); // Resize memory to hold 5 integers

    if (arr == NULL) {
        printf("Memory reallocation failed\n");
        return 1;
    }

    for (int i = 3; i < 5; i++) {
        arr[i] = i + 1; // Assign values to new elements
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }

    free(arr); // Free allocated memory
    return 0;
}
```

## Comparison: malloc vs calloc vs realloc

| Feature              | malloc                     | calloc                     | realloc                    |
|----------------------|----------------------------|----------------------------|----------------------------|
| Initialization       | No (contains garbage)      | Yes (initialized to zero)  | Retains existing data      |
| Use Case             | Single memory block        | Array of elements          | Resize existing memory     |
| Syntax               | `malloc(size)`             | `calloc(num, size)`        | `realloc(ptr, new_size)`   |
| Return Value         | Pointer to memory block    | Pointer to memory block    | Pointer to resized block   |

## Summary
- Use `malloc` when you need a single block of memory without initialization.
- Use `calloc` when you need an array of memory initialized to zero.
- Use `realloc` to resize an existing memory block.

Understanding these functions is essential for efficient memory management in C programs.