# CMake and Comparison with Make

In this section, you will learn about CMake and how it compares to Make.

## What is CMake?

- CMake is a cross-platform build system generator.
- It generates build files (e.g., Makefiles, Ninja files, Visual Studio project files) for various platforms.
- It is not a build system itself but works with build systems like Make.

## Why Use CMake?

- Simplifies the build process for cross-platform projects.
- Automatically detects dependencies and configurations.
- Supports modern C++ standards and tools.

## Example: Simple CMake Project

### File Structure
```
project/
├── main.c
├── utils.c
├── utils.h
└── CMakeLists.txt
```

### main.c
```c
#include "utils.h"
#include <stdio.h>

int main() {
    printMessage();
    return 0;
}
```

### utils.c
```c
#include "utils.h"
#include <stdio.h>

void printMessage() {
    printf("Hello from utils!\n");
}
```

### utils.h
```c
#ifndef UTILS_H
#define UTILS_H

void printMessage();

#endif
```

### CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.10)

# Project name
project(MyProject)

# Set C standard
set(CMAKE_C_STANDARD 99)

# Add source files
add_executable(program main.c utils.c)
```

## Building with CMake

1. Create a `build` directory:
   ```bash
   mkdir build && cd build
   ```
2. Generate build files:
   ```bash
   cmake ..
   ```
3. Build the project:
   ```bash
   make
   ```
4. Run the program:
   ```bash
   ./program
   ```

## Comparison: Make vs CMake

| Feature                | Make                          | CMake                         |
|------------------------|-------------------------------|-------------------------------|
| Type                  | Build system                  | Build system generator        |
| Cross-Platform Support | Limited                       | Excellent                     |
| Dependency Management  | Manual                       | Automatic                     |
| Ease of Use            | Simple for small projects     | Better for large projects     |
| Output                | Directly builds the project   | Generates build files (e.g., Makefiles) |
| Flexibility            | Limited to Makefiles          | Supports multiple build systems (e.g., Ninja, Visual Studio) |

## Exercise

1. Create a simple project with CMake and build it using Make.
2. Experiment with adding compiler flags in `CMakeLists.txt`.
3. Compare the workflow of Make and CMake for the same project.