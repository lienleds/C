# Constants

In this section, you will learn about constants in C.

## Topics

- Declaring Constants
- `const` Keyword
- `#define` Preprocessor Directive

## Example

```c
#include <stdio.h>

#define PI 3.14 // Preprocessor constant

int main() {
    const int DAYS_IN_WEEK = 7; // Constant variable

    printf("Pi: %.2f\n", PI);
    printf("Days in a week: %d\n", DAYS_IN_WEEK);

    return 0;
}
```

## Exercise

1. Declare constants using `const` and `#define`.
2. Print their values.
3. Experiment with modifying constants (observe errors).