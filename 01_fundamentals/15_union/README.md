# Unions

In this section, you will learn about unions in C.

## Topics

- Declaring and Using Unions
- Differences Between Structs and Unions
- Use Cases

## Example: Union

```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;

    data.i = 10;
    printf("data.i: %d\n", data.i);

    data.f = 220.5;
    printf("data.f: %.2f\n", data.f);

    snprintf(data.str, sizeof(data.str), "Hello");
    printf("data.str: %s\n", data.str);

    return 0;
}
```

## Explanation

- A `union` is a user-defined data type similar to a `struct`, but all members share the same memory location.
- Only one member can hold a value at a time.
- The size of a union is determined by the size of its largest member.

## Schema: Struct vs Union

This schema provides a visual comparison between structs and unions to help understand their differences.

```plaintext
+-------------------+-------------------+
|      Struct       |      Union        |
+-------------------+-------------------+
| Memory:           | Memory:           |
| Each member has   | All members share |
| its own memory.   | the same memory.  |
+-------------------+-------------------+
| Size:             | Size:             |
| Sum of all        | Size of the       |
| members' sizes.   | largest member.   |
+-------------------+-------------------+
| Use Case:         | Use Case:         |
| Grouping related  | Saving memory     |
| data.             | when only one     |
|                   | value is used at  |
|                   | a time.           |
+-------------------+-------------------+
```

### Example: Memory Allocation

#### Struct
```c
struct Example {
    int i;    // 4 bytes
    float f;  // 4 bytes
    char c;   // 1 byte
};
// Total size: 12 bytes (including padding)
```

#### Union
```c
union Example {
    int i;    // 4 bytes
    float f;  // 4 bytes
    char c;   // 1 byte
};
// Total size: 4 bytes (size of the largest member)
```

### Summary
- **Structs** are ideal for grouping related data where all members are used simultaneously.
- **Unions** are useful for saving memory when only one member is used at a time.

### Differences Between Structs and Unions

| Feature       | Struct                     | Union                     |
|---------------|----------------------------|---------------------------|
| Memory        | Each member has its own memory. | All members share the same memory. |
| Size          | Sum of all members' sizes. | Size of the largest member. |
| Use Case      | Grouping related data.     | Saving memory when only one value is used at a time. |

## Exercise

1. Create a union with multiple data types and observe its size.
2. Assign values to different members and observe the behavior.
3. Discuss scenarios where unions are useful (e.g., embedded systems).