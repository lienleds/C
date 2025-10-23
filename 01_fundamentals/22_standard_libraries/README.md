# Standard C Libraries

The C Standard Library provides a collection of functions and macros that simplify common programming tasks. These libraries are essential for performing input/output operations, string manipulation, memory management, and more.

## Common Libraries

### 1. `<stdio.h>`
- Provides functions for input and output.
- Common functions:
  - `printf`: Prints formatted output to the console.
  - `scanf`: Reads formatted input from the console.
  - `fopen`, `fclose`: File handling functions.

### 2. `<stdlib.h>`
- Provides functions for memory allocation, process control, and conversions.
- Common functions:
  - `malloc`, `calloc`, `realloc`, `free`: Dynamic memory management.
  - `atoi`, `atof`: Convert strings to integers or floats.
  - `exit`: Terminates the program.

### 3. `<string.h>`
- Provides functions for string manipulation.
- Common functions:
  - `strlen`: Returns the length of a string.
  - `strcpy`, `strncpy`: Copies strings.
  - `strcmp`, `strncmp`: Compares strings.
  - `strcat`, `strncat`: Concatenates strings.

### 4. `<math.h>`
- Provides mathematical functions.
- Common functions:
  - `sqrt`: Computes the square root.
  - `pow`: Computes the power of a number.
  - `sin`, `cos`, `tan`: Trigonometric functions.

## Example: Using `<stdio.h>` and `<stdlib.h>`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr;
    int n = 5;

    // Dynamically allocate memory
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    // Initialize and print array
    for (int i = 0; i < n; i++) {
        arr[i] = i * i;
        printf("arr[%d] = %d\n", i, arr[i]);
    }

    // Free allocated memory
    free(arr);

    return 0;
}
```

## Exercise
1. Write a program that uses `<string.h>` to manipulate strings.
2. Use `<math.h>` to calculate the area of a circle given its radius.
3. Experiment with file handling functions from `<stdio.h>`.

## Summary
The C Standard Library is a powerful tool that provides essential functions for various programming tasks. Familiarity with these libraries is crucial for efficient and effective C programming.