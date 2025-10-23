# Error Handling in C

Error handling is an essential aspect of programming that ensures a program can gracefully handle unexpected situations and provide meaningful feedback to the user. In C, error handling is typically done using return codes, global variables, and standard library functions.

## Common Error Handling Techniques

### 1. Return Codes
Functions in C often return an integer value to indicate success or failure. A return value of `0` usually indicates success, while non-zero values indicate an error.

#### Example
```c
#include <stdio.h>

int divide(int a, int b, int *result) {
    if (b == 0) {
        return -1; // Error: Division by zero
    }
    *result = a / b;
    return 0; // Success
}

int main() {
    int result;
    if (divide(10, 0, &result) != 0) {
        printf("Error: Division by zero\n");
    } else {
        printf("Result: %d\n", result);
    }
    return 0;
}
```

### 2. Global Variable `errno`
The `errno` variable, defined in `<errno.h>`, is set by system calls and some library functions to indicate the error code.

#### Example
```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

int main() {
    FILE *file = fopen("nonexistent.txt", "r");
    if (file == NULL) {
        printf("Error: %s\n", strerror(errno));
    }
    return 0;
}
```

### 3. `perror` Function
The `perror` function prints a descriptive error message to `stderr` based on the current value of `errno`.

#### Example
```c
#include <stdio.h>
#include <errno.h>

int main() {
    FILE *file = fopen("nonexistent.txt", "r");
    if (file == NULL) {
        perror("File open error");
    }
    return 0;
}
```

### 4. Assertions
The `assert` macro, defined in `<assert.h>`, is used to check assumptions in the code. If the condition evaluates to false, the program terminates with an error message.

#### Example
```c
#include <stdio.h>
#include <assert.h>

int main() {
    int x = 5;
    assert(x > 0); // Passes
    assert(x < 0); // Fails and terminates the program
    return 0;
}
```

### 5. Custom Error Messages
You can define custom error messages and codes to handle application-specific errors.

#### Example
```c
#include <stdio.h>

#define FILE_NOT_FOUND 1
#define PERMISSION_DENIED 2

void print_error(int error_code) {
    switch (error_code) {
        case FILE_NOT_FOUND:
            printf("Error: File not found\n");
            break;
        case PERMISSION_DENIED:
            printf("Error: Permission denied\n");
            break;
        default:
            printf("Error: Unknown error\n");
    }
}

int main() {
    print_error(FILE_NOT_FOUND);
    return 0;
}
```

## Best Practices
1. **Check Return Values**:
   - Always check the return values of functions, especially system calls and library functions.

2. **Use Meaningful Error Codes**:
   - Define and document error codes for your application.

3. **Log Errors**:
   - Log errors to a file or console for debugging and auditing.

4. **Fail Gracefully**:
   - Ensure the program can recover from errors or terminate gracefully.

5. **Avoid Silent Failures**:
   - Always provide meaningful feedback to the user when an error occurs.

## Exercises

1. Write a program that opens a file and handles errors such as file not found or permission denied.
2. Implement a function that divides two numbers and handles division by zero using return codes.
3. Use `errno` and `perror` to handle errors in file operations.
4. Create a custom error handling mechanism for a simple application.

## Additional Resources

- [C Error Handling](https://en.cppreference.com/w/c/error)
- [GNU C Library: Error Reporting](https://www.gnu.org/software/libc/manual/html_node/Error-Reporting.html)
- [Assertions in C](https://en.wikipedia.org/wiki/Assertion_(software_development))