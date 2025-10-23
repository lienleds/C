# Signals in C

Signals are a mechanism in Unix-like operating systems for notifying a process that a specific event has occurred. They are used for inter-process communication (IPC) and handling asynchronous events.

## Key Concepts

1. **Signal Types**:
   - Signals are identified by integer numbers (e.g., `SIGINT`, `SIGTERM`, `SIGKILL`).

2. **Signal Handlers**:
   - A signal handler is a function that is executed when a specific signal is received.

3. **Default Actions**:
   - Each signal has a default action, such as terminating the process or ignoring the signal.

4. **Asynchronous Nature**:
   - Signals can interrupt the normal flow of a program at any time.

## Common Signals

| Signal   | Description                          |
|----------|--------------------------------------|
| `SIGINT` | Interrupt signal (Ctrl+C).           |
| `SIGTERM`| Termination signal.                  |
| `SIGKILL`| Kill signal (cannot be caught).      |
| `SIGSEGV`| Segmentation fault.                  |
| `SIGHUP` | Hangup signal.                       |
| `SIGCHLD`| Child process terminated.            |

## Signal Handling

1. **Default Handling**:
   - The operating system performs the default action for the signal.

2. **Custom Handling**:
   - A program can define a custom signal handler using the `signal` function.

3. **Ignoring Signals**:
   - Signals can be ignored by setting their handler to `SIG_IGN`.

## Example: Custom Signal Handler

The following example demonstrates how to handle the `SIGINT` signal (Ctrl+C) using a custom signal handler.

### Code Example

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void handle_sigint(int sig) {
    printf("Caught signal %d (SIGINT). Exiting gracefully.\n", sig);
    exit(0);
}

int main() {
    // Register the signal handler for SIGINT
    signal(SIGINT, handle_sigint);

    printf("Press Ctrl+C to trigger SIGINT.\n");

    while (1) {
        printf("Running...\n");
        sleep(1);
    }

    return 0;
}
```

## Example: Ignoring a Signal

The following example demonstrates how to ignore the `SIGINT` signal.

```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int main() {
    // Ignore the SIGINT signal
    signal(SIGINT, SIG_IGN);

    printf("SIGINT is ignored. Press Ctrl+C, but nothing will happen.\n");

    while (1) {
        printf("Running...\n");
        sleep(1);
    }

    return 0;
}
```

## Example: Handling Multiple Signals

The following example demonstrates how to handle multiple signals (`SIGINT` and `SIGTERM`) using custom signal handlers.

### Code Example

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void handle_sigint(int sig) {
    printf("Caught signal %d (SIGINT). Exiting gracefully.\n", sig);
    exit(0);
}

void handle_sigterm(int sig) {
    printf("Caught signal %d (SIGTERM). Performing cleanup.\n", sig);
    // Perform cleanup tasks here
    exit(0);
}

int main() {
    // Register the signal handlers for SIGINT and SIGTERM
    signal(SIGINT, handle_sigint);
    signal(SIGTERM, handle_sigterm);

    printf("Press Ctrl+C to trigger SIGINT or send SIGTERM to terminate.\n");

    while (1) {
        printf("Running...\n");
        sleep(1);
    }

    return 0;
}
```

## Best Practices

1. **Use Signal Handlers Sparingly**:
   - Signals are asynchronous and can interrupt the program at any time, making them difficult to debug.

2. **Avoid Complex Logic in Handlers**:
   - Keep signal handlers simple and avoid using non-reentrant functions.

3. **Restore Default Behavior**:
   - Restore the default behavior for signals when appropriate.

4. **Use `sigaction` for Portability**:
   - The `sigaction` function provides more control and is preferred over `signal`.

## Use Cases

- Gracefully terminating a program (e.g., handling `SIGINT`).
- Cleaning up resources when a process is terminated.
- Notifying a parent process when a child process exits.

Signals are a powerful tool for handling asynchronous events in C programs. However, they should be used carefully due to their asynchronous nature.