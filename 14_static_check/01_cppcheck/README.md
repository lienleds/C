# Cppcheck

Cppcheck is a static analysis tool for C and C++ code. It focuses on detecting bugs, undefined behavior, and potential security vulnerabilities. Unlike compilers, Cppcheck does not check for syntax errors but instead analyzes the code for logical issues.

## Key Features
- **Detects Bugs**: Identifies null pointer dereferences, memory leaks, and buffer overflows.
- **Coding Standards**: Supports MISRA C and other coding standards.
- **Customizable Checks**: Allows users to define their own rules.
- **Platform Independent**: Works on Linux, macOS, and Windows.

## Installation

### On Linux
```bash
sudo apt-get update
sudo apt-get install cppcheck
```

### On macOS
```bash
brew install cppcheck
```

### From Source
1. Clone the repository:
   ```bash
   git clone https://github.com/danmar/cppcheck.git
   ```
2. Build and install:
   ```bash
   cd cppcheck
   make
   sudo make install
   ```

## Usage
To analyze a C or C++ file, use the following command:
```bash
cppcheck your_code.c
```

### Common Options
- `--enable=all`: Enables all checks, including style and performance.
- `--std=c99`: Specifies the C standard (e.g., C99, C11).
- `--language=c++`: Specifies the language (C or C++).
- `--output-file=<file>`: Redirects output to a file.

### Example
Consider the following C program:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = malloc(sizeof(int));
    *ptr = 10;
    printf("Value: %d\n", *ptr);
    // Forgot to free memory
    return 0;
}
```
Run Cppcheck:
```bash
cppcheck --enable=all example.c
```
Output:
```
[example.c:8]: (error) Memory leak: ptr
```

## Integrating with Build Systems
- **Makefiles**: Add Cppcheck as a target in your Makefile.
- **CI/CD Pipelines**: Integrate Cppcheck into Jenkins, GitHub Actions, or other CI tools.

## Best Practices
- Run Cppcheck regularly during development.
- Use `--enable=all` for comprehensive analysis.
- Address warnings and errors promptly.
- Combine Cppcheck with other tools like Valgrind for thorough analysis.

## Additional Resources
- [Cppcheck Official Website](http://cppcheck.sourceforge.net/)
- [Cppcheck GitHub Repository](https://github.com/danmar/cppcheck)
- [Cppcheck Documentation](http://cppcheck.sourceforge.net/manual.pdf)