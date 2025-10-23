# Inline Assembly in C

Inline assembly allows embedding assembly language instructions directly within C code. It is useful for performance-critical applications, hardware-specific operations, and low-level programming tasks.

## Why Use Inline Assembly?
- **Performance Optimization**: Achieve better performance by writing critical sections in assembly.
- **Hardware Access**: Perform operations that are not directly supported by C.
- **Custom Instructions**: Use processor-specific instructions for specialized tasks.

## Syntax
The syntax for inline assembly in C depends on the compiler. The most common syntax is provided by GCC (GNU Compiler Collection).

### GCC Inline Assembly Syntax
```c
asm("assembly-instruction" : output-operands : input-operands : clobbered-registers);
```

### Components
1. **Assembly Instruction**: The actual assembly code to execute.
2. **Output Operands**: Variables modified by the assembly code.
3. **Input Operands**: Variables used as input to the assembly code.
4. **Clobbered Registers**: Registers modified by the assembly code.

## Examples

### 1. Simple Inline Assembly
```c
#include <stdio.h>

int main() {
    int a = 10, b = 20, result;
    asm("addl %%ebx, %%eax" : "=a"(result) : "a"(a), "b"(b));
    printf("Result: %d\n", result);
    return 0;
}
```

### 2. Accessing CPU Registers
```c
#include <stdio.h>

int main() {
    int value;
    asm("movl $42, %0" : "=r"(value));
    printf("Value: %d\n", value);
    return 0;
}
```

### 3. Using Clobbered Registers
```c
#include <stdio.h>

int main() {
    int a = 5, b = 3, result;
    asm("imull %%ebx, %%eax" : "=a"(result) : "a"(a), "b"(b) : "cc");
    printf("Multiplication Result: %d\n", result);
    return 0;
}
```

### 4. Inline Assembly for Hardware Access
```c
#include <stdio.h>

int main() {
    asm("hlt"); // Halts the CPU
    return 0;
}
```

## Best Practices
1. **Use Sparingly**:
   - Inline assembly should be used only when necessary. Prefer C for portability and maintainability.

2. **Document Code**:
   - Clearly document the purpose of the assembly code.

3. **Test Thoroughly**:
   - Inline assembly can introduce subtle bugs. Test thoroughly on the target hardware.

4. **Understand the Compiler**:
   - Inline assembly syntax and behavior can vary between compilers.

## Exercises

1. Write a program that swaps two integers using inline assembly.
2. Implement a function to calculate the factorial of a number using assembly instructions.
3. Use inline assembly to read the CPU's timestamp counter.
4. Explore the effect of clobbered registers on program behavior.

## Additional Resources

- [GCC Inline Assembly](https://gcc.gnu.org/onlinedocs/gcc/Using-Assembly-Language-with-C.html)
- [Introduction to x86 Assembly](https://en.wikipedia.org/wiki/X86_assembly_language)
- [Low-Level Programming in C](https://www.tutorialspoint.com/cprogramming/c_inline_assembly.htm)