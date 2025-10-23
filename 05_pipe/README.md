# Pipes in C

Pipes are a mechanism for inter-process communication (IPC) that allow data to be passed from one process to another. Pipes are unidirectional, meaning data flows in one direction only. They are commonly used for communication between a parent process and its child processes.

## Key Concepts

1. **Unidirectional Communication**:
   - Data flows in one direction: from the write end to the read end.

2. **Anonymous Pipes**:
   - Pipes created using the `pipe` system call are anonymous and exist only while the processes are running.

3. **Named Pipes (FIFOs)**:
   - Named pipes are persistent and can be used for communication between unrelated processes.

4. **Blocking Behavior**:
   - Reading from an empty pipe or writing to a full pipe causes the process to block until the operation can proceed.

## How Pipes Work

1. **Create a Pipe**:
   - Use the `pipe` system call to create a pipe.

2. **Fork a Process**:
   - Use the `fork` system call to create a child process.

3. **Close Unused Ends**:
   - Close the write end in the reading process and the read end in the writing process.

4. **Read and Write Data**:
   - Use `read` and `write` system calls to transfer data through the pipe.

## Example: Anonymous Pipe

The following example demonstrates how a parent process can send data to a child process using a pipe.

### Code Example

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>

int main() {
    int pipefd[2];
    pid_t pid;
    char write_msg[] = "Hello, Pipe!";
    char read_msg[100];

    // Create a pipe
    if (pipe(pipefd) == -1) {
        perror("pipe");
        exit(EXIT_FAILURE);
    }

    // Fork a child process
    pid = fork();

    if (pid < 0) {
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (pid == 0) {
        // Child process: Read from the pipe
        close(pipefd[1]); // Close unused write end
        read(pipefd[0], read_msg, sizeof(read_msg));
        printf("Child received: %s\n", read_msg);
        close(pipefd[0]);
    } else {
        // Parent process: Write to the pipe
        close(pipefd[0]); // Close unused read end
        write(pipefd[1], write_msg, strlen(write_msg) + 1);
        close(pipefd[1]);
    }

    return 0;
}
```

## Advantages

- Simple and efficient for parent-child communication.
- No need for explicit synchronization mechanisms.

## Disadvantages

- Unidirectional communication.
- Limited to processes on the same machine.
- Anonymous pipes cannot be used between unrelated processes.

## Named Pipes (FIFOs)

Named pipes, also known as FIFOs, are a special type of file that allows bidirectional communication between unrelated processes. They are created using the `mkfifo` system call or the `mknod` command.

### Example: Named Pipe

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <unistd.h>
#include <string.h>

#define FIFO_NAME "myfifo"

int main() {
    int fd;
    char write_msg[] = "Hello, FIFO!";
    char read_msg[100];

    // Create a named pipe
    mkfifo(FIFO_NAME, 0666);

    if (fork() == 0) {
        // Child process: Read from the FIFO
        fd = open(FIFO_NAME, O_RDONLY);
        read(fd, read_msg, sizeof(read_msg));
        printf("Child received: %s\n", read_msg);
        close(fd);
    } else {
        // Parent process: Write to the FIFO
        fd = open(FIFO_NAME, O_WRONLY);
        write(fd, write_msg, strlen(write_msg) + 1);
        close(fd);
    }

    // Remove the FIFO
    unlink(FIFO_NAME);

    return 0;
}
```

## Use Cases

- Communication between parent and child processes.
- Data transfer between unrelated processes using named pipes.

Pipes are a fundamental IPC mechanism in Unix-like systems, providing a simple and efficient way to transfer data between processes.