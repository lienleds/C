# Program Memory Layout Schema

Below is a visual representation of the memory layout of a program:

```
+-----------------------+
|       Stack          |
| - Local Variables    |
| - Function Calls     |
| - Return Addresses   |
| Grows Downwards      |
+-----------------------+
|       Heap           |
| - Dynamically        |
|   Allocated Memory   |
| Grows Upwards        |
+-----------------------+
|       BSS            |
| - Uninitialized      |
|   Global/Static Vars |
+-----------------------+
|       Data           |
| - Initialized        |
|   Global/Static Vars |
+-----------------------+
|       Text           |
| - Executable Code    |
| - Read-Only          |
+-----------------------+
```

## Explanation

1. **Text Segment**:
   - Contains the program's machine code (instructions).
   - Read-only to prevent accidental modification.

2. **Data Segment**:
   - Stores global and static variables that are initialized.

3. **BSS Segment**:
   - Stores global and static variables that are uninitialized or initialized to zero.

4. **Heap Segment**:
   - Used for dynamic memory allocation (e.g., `malloc`, `calloc`).
   - Grows upwards as memory is allocated.

5. **Stack Segment**:
   - Stores local variables, function call information, and return addresses.
   - Grows downwards as functions are called.

## Key Points

- The **stack** and **heap** grow towards each other.
- The **text**, **data**, and **BSS** segments are fixed in size at runtime.
- Understanding this layout is crucial for debugging and optimizing memory usage.

## Exercise

1. Draw the memory layout for a sample program and identify where each variable is stored.
2. Use debugging tools like `gdb` to inspect memory segments during runtime.
3. Experiment with stack and heap overflows to understand their behavior.