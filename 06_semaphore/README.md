# Semaphores in C

Semaphores are synchronization primitives used to control access to shared resources in concurrent programming. They are commonly used to prevent race conditions and ensure that multiple processes or threads can safely access shared resources.

## Key Concepts

1. **Binary Semaphore**:
   - Also known as a mutex, it can have only two values: 0 (locked) and 1 (unlocked).

2. **Counting Semaphore**:
   - Can have a value greater than 1, allowing multiple processes or threads to access the resource up to a specified limit.

3. **Operations**:
   - **Wait (P)**: Decrements the semaphore value. If the value is 0, the process is blocked until the semaphore becomes available.
   - **Signal (V)**: Increments the semaphore value, signaling that the resource is available.

4. **System Calls**:
   - Semaphores in C are implemented using system calls like `sem_init`, `sem_wait`, `sem_post`, and `sem_destroy`.

## How Semaphores Work

1. **Initialize the Semaphore**:
   - Use `sem_init` to initialize the semaphore.

2. **Wait for the Semaphore**:
   - Use `sem_wait` to decrement the semaphore value and block if the value is 0.

3. **Signal the Semaphore**:
   - Use `sem_post` to increment the semaphore value and unblock waiting processes.

4. **Destroy the Semaphore**:
   - Use `sem_destroy` to clean up the semaphore.

## Example: Semaphore in C

The following example demonstrates how to use a semaphore to synchronize access to a shared resource between multiple threads.

### Code Example

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

#define NUM_THREADS 5

sem_t semaphore;

void* thread_function(void* arg) {
    int thread_id = *(int*)arg;

    printf("Thread %d: Waiting for semaphore\n", thread_id);
    sem_wait(&semaphore);

    printf("Thread %d: Acquired semaphore\n", thread_id);
    sleep(1); // Simulate work

    printf("Thread %d: Releasing semaphore\n", thread_id);
    sem_post(&semaphore);

    return NULL;
}

int main() {
    pthread_t threads[NUM_THREADS];
    int thread_ids[NUM_THREADS];

    // Initialize the semaphore with a value of 2
    sem_init(&semaphore, 0, 2);

    // Create threads
    for (int i = 0; i < NUM_THREADS; i++) {
        thread_ids[i] = i;
        pthread_create(&threads[i], NULL, thread_function, &thread_ids[i]);
    }

    // Wait for threads to finish
    for (int i = 0; i < NUM_THREADS; i++) {
        pthread_join(threads[i], NULL);
    }

    // Destroy the semaphore
    sem_destroy(&semaphore);

    return 0;
}
```

## Advantages

- Prevents race conditions by controlling access to shared resources.
- Simple and efficient for synchronization.

## Disadvantages

- Can lead to deadlocks if not used carefully.
- Requires careful design to avoid performance bottlenecks.

## Use Cases

- Synchronizing access to shared resources in multithreaded programs.
- Implementing producer-consumer problems.
- Controlling access to limited resources, such as database connections.

Semaphores are a fundamental tool for synchronization in concurrent programming. They provide a simple and effective way to manage access to shared resources and ensure data consistency.