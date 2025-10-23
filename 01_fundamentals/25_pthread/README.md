# Pthreads in C

In this section, you will learn about POSIX threads (pthreads) in C, including thread creation, synchronization, and common use cases.

## What are Pthreads?
- Pthreads (POSIX threads) are a standard for multithreading in C.
- They allow a program to perform multiple tasks concurrently by creating and managing threads.

## Key Functions

### 1. `pthread_create`
- Creates a new thread.
- Syntax:
  ```c
  int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine)(void *), void *arg);
  ```

### 2. `pthread_join`
- Waits for a thread to terminate.
- Syntax:
  ```c
  int pthread_join(pthread_t thread, void **retval);
  ```
- **Explanation**: The `pthread_join` function blocks the calling thread until the specified thread terminates. It is used to ensure that resources are properly cleaned up and that the main thread waits for other threads to complete their tasks.
- **Use Case**: Joining threads is essential when the main thread depends on the results of other threads or when proper cleanup is required.

### 3. `pthread_detach`
- Detaches a thread, allowing it to run independently.
- Syntax:
  ```c
  int pthread_detach(pthread_t thread);
  ```
- **Explanation**: The `pthread_detach` function marks a thread as detached, meaning its resources will be automatically released when it terminates. Detached threads cannot be joined.
- **Use Case**: Detaching threads is useful for background tasks where the main thread does not need to wait for their completion.

### 4. `pthread_mutex_lock` and `pthread_mutex_unlock`
- Used for thread synchronization to prevent race conditions.
- Syntax:
  ```c
  int pthread_mutex_lock(pthread_mutex_t *mutex);
  int pthread_mutex_unlock(pthread_mutex_t *mutex);
  ```

## Example: Thread Creation

```c
#include <stdio.h>
#include <pthread.h>

void *printMessage(void *arg) {
    printf("Hello from thread!\n");
    return NULL;
}

int main() {
    pthread_t thread;

    // Create a new thread
    if (pthread_create(&thread, NULL, printMessage, NULL) != 0) {
        printf("Error creating thread\n");
        return 1;
    }

    // Wait for the thread to finish
    pthread_join(thread, NULL);

    printf("Thread has finished\n");
    return 0;
}
```

## Example: Thread Synchronization

```c
#include <stdio.h>
#include <pthread.h>

#define NUM_THREADS 5

pthread_mutex_t mutex;
int counter = 0;

void *incrementCounter(void *arg) {
    pthread_mutex_lock(&mutex);
    counter++;
    printf("Counter: %d\n", counter);
    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main() {
    pthread_t threads[NUM_THREADS];
    pthread_mutex_init(&mutex, NULL);

    for (int i = 0; i < NUM_THREADS; i++) {
        pthread_create(&threads[i], NULL, incrementCounter, NULL);
    }

    for (int i = 0; i < NUM_THREADS; i++) {
        pthread_join(threads[i], NULL);
    }

    pthread_mutex_destroy(&mutex);
    return 0;
}
```

## Explanation
- **Thread Creation**: Use `pthread_create` to create threads and `pthread_join` to wait for them to finish.
- **Synchronization**: Use mutexes (`pthread_mutex_lock` and `pthread_mutex_unlock`) to prevent race conditions when accessing shared resources.

## Exercise
1. Create a program that spawns multiple threads to perform a task concurrently.
2. Use mutexes to synchronize access to shared resources.
3. Experiment with thread attributes (e.g., detached threads).

## Summary
Pthreads provide a powerful way to implement multithreading in C. Understanding thread creation, synchronization, and proper resource management is essential for writing efficient and safe multithreaded programs.