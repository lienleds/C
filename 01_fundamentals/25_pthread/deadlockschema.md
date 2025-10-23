# Deadlock Schema

This schema illustrates the concept of deadlock in multithreaded programs, highlighting the conditions that lead to deadlock and how to avoid it.

## Deadlock Conditions

A deadlock occurs when the following four conditions are met simultaneously:

1. **Mutual Exclusion**
   - Only one thread can hold a resource at a time.

2. **Hold and Wait**
   - A thread holding at least one resource is waiting to acquire additional resources held by other threads.

3. **No Preemption**
   - Resources cannot be forcibly taken from threads; they must be released voluntarily.

4. **Circular Wait**
   - A set of threads are waiting on each other in a circular chain.

## Visual Representation of Deadlock

```plaintext
Thread 1          Thread 2
   |                 |
   v                 v
+-------+         +-------+
|Mutex A|         |Mutex B|
+-------+         +-------+
   ^                 ^
   |                 |
   +-----------------+
```

In this scenario:
- Thread 1 locks Mutex A and waits for Mutex B.
- Thread 2 locks Mutex B and waits for Mutex A.
- Both threads are stuck, resulting in a deadlock.

## Example Workflow Leading to Deadlock

1. **Thread 1** locks Mutex A.
2. **Thread 2** locks Mutex B.
3. **Thread 1** tries to lock Mutex B but is blocked because Thread 2 holds it.
4. **Thread 2** tries to lock Mutex A but is blocked because Thread 1 holds it.

## Avoiding Deadlock

### 1. Lock Ordering
- Always acquire locks in a consistent global order.

### 2. Timeout Mechanism
- Use timed mutexes to avoid indefinite blocking.

### 3. Deadlock Detection
- Implement algorithms to detect and recover from deadlocks.

### 4. Try Lock
- Use `pthread_mutex_trylock` to attempt locking without blocking.

## Deadlock-Free Example

```c
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t mutex1, mutex2;

void *thread1(void *arg) {
    pthread_mutex_lock(&mutex1);
    printf("Thread 1: Locked mutex1\n");

    pthread_mutex_lock(&mutex2);
    printf("Thread 1: Locked mutex2\n");

    pthread_mutex_unlock(&mutex2);
    pthread_mutex_unlock(&mutex1);

    return NULL;
}

void *thread2(void *arg) {
    pthread_mutex_lock(&mutex1);
    printf("Thread 2: Locked mutex1\n");

    pthread_mutex_lock(&mutex2);
    printf("Thread 2: Locked mutex2\n");

    pthread_mutex_unlock(&mutex2);
    pthread_mutex_unlock(&mutex1);

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

## Summary
This schema provides a clear understanding of deadlock, its conditions, and strategies to avoid it. By following best practices, you can write robust multithreaded programs that are free from deadlocks.