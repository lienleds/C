# Mutex in Pthreads

Mutex (short for mutual exclusion) is a synchronization primitive used to prevent race conditions by ensuring that only one thread can access a critical section at a time.

## Key Functions

### 1. `pthread_mutex_init`
- Initializes a mutex.
- Syntax:
  ```c
  int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr);
  ```

### 2. `pthread_mutex_lock`
- Locks a mutex. If the mutex is already locked, the calling thread blocks until it becomes available.
- Syntax:
  ```c
  int pthread_mutex_lock(pthread_mutex_t *mutex);
  ```

### 3. `pthread_mutex_unlock`
- Unlocks a mutex, allowing other threads to acquire it.
- Syntax:
  ```c
  int pthread_mutex_unlock(pthread_mutex_t *mutex);
  ```

### 4. `pthread_mutex_destroy`
- Destroys a mutex, releasing its resources.
- Syntax:
  ```c
  int pthread_mutex_destroy(pthread_mutex_t *mutex);
  ```

## Example: Using Mutex

```c
#include <stdio.h>
#include <pthread.h>

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
    pthread_t threads[5];
    pthread_mutex_init(&mutex, NULL);

    for (int i = 0; i < 5; i++) {
        pthread_create(&threads[i], NULL, incrementCounter, NULL);
    }

    for (int i = 0; i < 5; i++) {
        pthread_join(threads[i], NULL);
    }

    pthread_mutex_destroy(&mutex);
    return 0;
}
```

## Deadlock

Deadlock occurs when two or more threads are waiting for each other to release a resource, resulting in a situation where none of the threads can proceed.

### Example of Deadlock

```c
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t mutex1, mutex2;

void *thread1(void *arg) {
    pthread_mutex_lock(&mutex1);
    printf("Thread 1: Locked mutex1\n");

    // Simulate some work
    sleep(1);

    pthread_mutex_lock(&mutex2);
    printf("Thread 1: Locked mutex2\n");

    pthread_mutex_unlock(&mutex2);
    pthread_mutex_unlock(&mutex1);

    return NULL;
}

void *thread2(void *arg) {
    pthread_mutex_lock(&mutex2);
    printf("Thread 2: Locked mutex2\n");

    // Simulate some work
    sleep(1);

    pthread_mutex_lock(&mutex1);
    printf("Thread 2: Locked mutex1\n");

    pthread_mutex_unlock(&mutex1);
    pthread_mutex_unlock(&mutex2);

    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_mutex_init(&mutex1, NULL);
    pthread_mutex_init(&mutex2, NULL);

    pthread_create(&t1, NULL, thread1, NULL);
    pthread_create(&t2, NULL, thread2, NULL);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    pthread_mutex_destroy(&mutex1);
    pthread_mutex_destroy(&mutex2);

    return 0;
}
```

### Avoiding Deadlock

1. **Lock Ordering**: Always acquire locks in a consistent order.
2. **Timeouts**: Use timed mutexes to avoid indefinite blocking.
3. **Try Lock**: Use `pthread_mutex_trylock` to attempt locking without blocking.

## Summary
Mutexes are essential for synchronizing threads and preventing race conditions. However, improper use can lead to deadlocks. Understanding and applying best practices is crucial for writing robust multithreaded programs.