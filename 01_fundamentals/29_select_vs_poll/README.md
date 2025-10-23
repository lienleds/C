# `select` vs `poll` in C

In this section, you will learn about the differences between `select` and `poll` system calls in C, their usage, and their advantages and disadvantages.

## What is `select`?
- `select` is a system call used to monitor multiple file descriptors to see if they are ready for I/O operations (read, write, or exceptions).
- It uses a fixed-size bitmask to represent file descriptors.
- Syntax:
  ```c
  int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
  ```

### Example: Using `select`
```c
#include <stdio.h>
#include <sys/select.h>
#include <unistd.h>

int main() {
    fd_set readfds;
    struct timeval timeout;
    int retval;

    FD_ZERO(&readfds);
    FD_SET(STDIN_FILENO, &readfds);

    timeout.tv_sec = 5;
    timeout.tv_usec = 0;

    printf("Waiting for input...\n");
    retval = select(STDIN_FILENO + 1, &readfds, NULL, NULL, &timeout);

    if (retval == -1) {
        perror("select");
    } else if (retval) {
        printf("Data is available now.\n");
    } else {
        printf("No data within five seconds.\n");
    }

    return 0;
}
```

## What is `poll`?
- `poll` is a system call used to monitor multiple file descriptors, similar to `select`.
- It uses an array of `struct pollfd` to represent file descriptors.
- Syntax:
  ```c
  int poll(struct pollfd *fds, nfds_t nfds, int timeout);
  ```

### Example: Using `poll`
```c
#include <stdio.h>
#include <poll.h>
#include <unistd.h>

int main() {
    struct pollfd fds[1];
    int retval;

    fds[0].fd = STDIN_FILENO;
    fds[0].events = POLLIN;

    printf("Waiting for input...\n");
    retval = poll(fds, 1, 5000);

    if (retval == -1) {
        perror("poll");
    } else if (retval) {
        printf("Data is available now.\n");
    } else {
        printf("No data within five seconds.\n");
    }

    return 0;
}
```

## Key Differences

| Feature              | `select`                        | `poll`                          |
|----------------------|----------------------------------|----------------------------------|
| Representation       | Fixed-size bitmask (`fd_set`).  | Dynamic array (`struct pollfd`).|
| Scalability          | Limited by `FD_SETSIZE`.        | Scales better for large sets.   |
| Timeout Resolution   | Microseconds (`struct timeval`).| Milliseconds (integer).         |
| Portability          | More portable.                  | Less portable.                  |

## Advantages and Disadvantages

### `select`
- **Advantages**:
  - Simple and widely supported.
  - Portable across different platforms.
- **Disadvantages**:
  - Limited by `FD_SETSIZE`.
  - Requires reinitializing `fd_set` after each call.

### `poll`
- **Advantages**:
  - Supports a larger number of file descriptors.
  - Does not require reinitialization of the `struct pollfd` array.
- **Disadvantages**:
  - Less portable than `select`.
  - Slightly more complex to use.

## Summary
- Use `select` for simpler applications with a small number of file descriptors.
- Use `poll` for applications that need to handle a larger number of file descriptors efficiently.