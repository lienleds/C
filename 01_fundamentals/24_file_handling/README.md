# File Handling

In this section, you will learn about file handling in C.

## Topics

- Reading and Writing Files
- File Pointers
- Error Handling

## Example

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "w");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    fprintf(file, "Hello, World!\n");
    fclose(file);

    return 0;
}
```

## Exercise

1. Write a program to read a file and print its contents.
2. Implement a program to append text to a file.
3. Create a program to count the number of lines in a file.