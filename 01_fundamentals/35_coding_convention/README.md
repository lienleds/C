# Coding Conventions in C

Coding conventions are a set of guidelines for writing code in a consistent and readable manner. Following these conventions improves code maintainability, readability, and collaboration among developers.

## General Guidelines

### 1. File Organization
- **File Naming**: Use lowercase letters with underscores (e.g., `my_program.c`).
- **Header Files**: Use `.h` extension for header files and include guards to prevent multiple inclusions.

#### Example
```c
#ifndef MY_HEADER_H
#define MY_HEADER_H

// Function declarations

#endif // MY_HEADER_H
```

### 2. Indentation
- Use 4 spaces per indentation level. Avoid using tabs.

#### Example
```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

### 3. Line Length
- Limit lines to 80 characters for better readability.

### 4. Comments
- Use comments to explain why the code does something, not what it does.
- Use `//` for single-line comments and `/* */` for multi-line comments.

#### Example
```c
// This function adds two numbers
int add(int a, int b) {
    return a + b;
}
```

## Naming Conventions

### 1. Variables
- Use descriptive names in `snake_case`.
- Use short names for loop counters (e.g., `i`, `j`).

#### Example
```c
int student_age;
int i;
```

### 2. Constants
- Use `UPPER_SNAKE_CASE` for constants.

#### Example
```c
#define MAX_BUFFER_SIZE 1024
```

### 3. Functions
- Use `snake_case` for function names.

#### Example
```c
int calculate_sum(int a, int b);
```

### 4. Structs and Enums
- Use `PascalCase` for struct and enum names.

#### Example
```c
typedef struct {
    int id;
    char name[50];
} Student;
```

## Best Practices

### 1. Error Handling
- Always check the return values of functions.

#### Example
```c
FILE *file = fopen("data.txt", "r");
if (file == NULL) {
    perror("Error opening file");
    return 1;
}
```

### 2. Avoid Magic Numbers
- Use constants or macros instead of hardcoding values.

#### Example
```c
#define PI 3.14159
float area = PI * radius * radius;
```

### 3. Modular Code
- Break code into smaller functions for better readability and reusability.

### 4. Initialize Variables
- Always initialize variables before use.

#### Example
```c
int count = 0;
```

### 5. Use Standard Libraries
- Prefer standard library functions over custom implementations.

## Exercises

1. Refactor a program to follow proper coding conventions.
2. Write a program that adheres to the naming conventions and formatting guidelines.
3. Create a header file with include guards and function declarations.
4. Identify and replace magic numbers in a given code snippet.

## Additional Resources

- [GNU Coding Standards](https://www.gnu.org/prep/standards/)
- [C Programming Style Guide](https://www.kernel.org/doc/html/latest/process/coding-style.html)
- [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)