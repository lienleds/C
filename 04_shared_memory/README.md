# Shared Memory in C

Shared memory is a method of inter-process communication (IPC) that allows multiple processes to access the same memory segment. It is one of the fastest IPC mechanisms because it avoids the overhead of data copying between processes.

## Key Concepts

1. **Memory Segment**:
   - A block of memory that can be shared between processes.

2. **Synchronization**:
   - Shared memory requires synchronization mechanisms (e.g., semaphores) to prevent race conditions.

3. **System Calls**:
   - Shared memory in C is implemented using system calls like `shmget`, `shmat`, `shmdt`, and `shmctl`.

## How Shared Memory Works

1. **Create a Shared Memory Segment**:
   - Use `shmget` to create a shared memory segment.

2. **Attach to the Segment**:
   - Use `shmat` to attach the shared memory segment to the process's address space.

3. **Access the Memory**:
   - Read from or write to the shared memory segment.

4. **Detach from the Segment**:
   - Use `shmdt` to detach the shared memory segment.

5. **Control the Segment**:
   - Use `shmctl` to perform control operations like deleting the segment.

## Example: Shared Memory in C

The following example demonstrates how two processes can communicate using shared memory.

### Code Example

#### Writer Process

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <string.h>

#define SHM_KEY 0x1234

int main() {
    int shmid;
    char *shared_memory;

    // Create shared memory segment
    shmid = shmget(SHM_KEY, 1024, IPC_CREAT | 0666);
    if (shmid < 0) {
        perror("shmget");
        exit(1);
    }

    // Attach to the shared memory segment
    shared_memory = (char *)shmat(shmid, NULL, 0);
    if (shared_memory == (char *)-1) {
        perror("shmat");
        exit(1);
    }

    // Write data to shared memory
    strcpy(shared_memory, "Hello, Shared Memory!");
    printf("Data written to shared memory: %s\n", shared_memory);

    // Detach from shared memory
    shmdt(shared_memory);

    return 0;
}
```

#### Reader Process

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <string.h>

#define SHM_KEY 0x1234

int main() {
    int shmid;
    char *shared_memory;

    // Locate the shared memory segment
    shmid = shmget(SHM_KEY, 1024, 0666);
    if (shmid < 0) {
        perror("shmget");
        exit(1);
    }

    // Attach to the shared memory segment
    shared_memory = (char *)shmat(shmid, NULL, 0);
    if (shared_memory == (char *)-1) {
        perror("shmat");
        exit(1);
    }

    // Read data from shared memory
    printf("Data read from shared memory: %s\n", shared_memory);

    // Detach from shared memory
    shmdt(shared_memory);

    return 0;
}
```

## Advantages

- High performance due to direct memory access.
- Suitable for large data transfers.

## Disadvantages

- Requires synchronization to prevent race conditions.
- Limited to processes on the same machine.

## Use Cases

- Inter-process communication in high-performance applications.
- Shared data structures like buffers and queues.

Shared memory is a powerful IPC mechanism, but it requires careful management to ensure data consistency and prevent conflicts.