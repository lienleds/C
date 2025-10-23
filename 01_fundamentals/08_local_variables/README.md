# Local Variables

In this section, you will learn about local variables in C.

## Topics

- Declaring Local Variables
- Scope and Lifetime
- Differences from Global Variables

## Example

```c
#include <stdio.h>

void display() {
    int localVar = 5; // Local variable
    printf("Local Variable: %d\n", localVar);
}

int main() {
    display();
    // printf("Local Variable in main: %d\n", localVar); // Error: localVar not accessible here
    return 0;
}
```

## Exercise

1. Declare local variables inside a function and use them.
2. Experiment with the scope of local variables.
3. Compare local and global variables in terms of scope and lifetime.