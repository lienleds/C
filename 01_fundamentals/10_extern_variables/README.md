# Extern Variables

In this section, you will learn about extern variables in C.

## Topics

- Declaring Extern Variables
- Scope and Lifetime
- Use Cases

## Example

### File 1: `file1.c`
```c
#include <stdio.h>

int externVar = 10; // Definition of extern variable

void display() {
    printf("Extern Variable: %d\n", externVar);
}
```

### File 2: `file2.c`
```c
#include <stdio.h>

extern int externVar; // Declaration of extern variable

int main() {
    printf("Extern Variable in main: %d\n", externVar);
    return 0;
}
```

## Exercise

1. Create two files and declare an extern variable in one file and use it in the other.
2. Experiment with modifying the extern variable in different files.
3. Discuss the advantages and disadvantages of using extern variables.