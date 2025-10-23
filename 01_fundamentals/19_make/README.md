# Make and Makefiles

In this section, you will learn about the `make` build system and how to use Makefiles in C projects.

## What is Make?

- `make` is a build automation tool that simplifies the process of compiling and linking programs.
- It uses a file called `Makefile` to define rules for building the project.

## Why Use Make?

- Automates repetitive compilation commands.
- Tracks dependencies and only rebuilds files that have changed.
- Simplifies the build process for large projects.

## Example: Simple Makefile

### File Structure
```
project/
├── main.c
├── utils.c
├── utils.h
└── Makefile
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

### Makefile
```make
# Compiler
CC = gcc

# Compiler flags
CFLAGS = -Wall -g

# Target executable
TARGET = program

# Source files
SRCS = main.c utils.c

# Object files
OBJS = $(SRCS:.c=.o)

# Build target
$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $(TARGET) $(OBJS)

# Clean up
clean:
	rm -f $(TARGET) $(OBJS)
```

## Explanation

1. **Variables**:
   - `CC`: Specifies the compiler (e.g., `gcc`).
   - `CFLAGS`: Compiler flags (e.g., `-Wall` for warnings, `-g` for debugging).
   - `TARGET`: The name of the output executable.
   - `SRCS`: List of source files.
   - `OBJS`: List of object files (derived from `SRCS`).

2. **Rules**:
   - `$(TARGET)`: The target executable depends on the object files.
   - `clean`: A special rule to remove generated files.

3. **Commands**:
   - Commands are indented with a **tab**, not spaces.
   - Example: `$(CC) $(CFLAGS) -o $(TARGET) $(OBJS)` compiles the object files into the executable.

## Running Make

1. Create the `Makefile` in the project directory.
2. Run `make` to build the project:
   ```bash
   make
   ```
3. Run the program:
   ```bash
   ./program
   ```
4. Clean up generated files:
   ```bash
   make clean
   ```

## Exercise

1. Create a simple project with multiple source files and a `Makefile`.
2. Add a `clean` rule to your `Makefile`.
3. Experiment with adding compiler flags (e.g., `-O2` for optimization).
4. Use `make -n` to preview the commands without executing them.