# Schema for Understanding Pthreads

This schema provides a structured overview of pthreads in C, making it easier to understand their key concepts and usage.

## Thread Lifecycle

1. **Thread Creation**
   - Function: `pthread_create`
   - Description: Creates a new thread.
   - State: New thread starts running.

2. **Thread Execution**
   - Function: Thread function (e.g., `void *start_routine(void *arg)`)
   - Description: The thread executes the specified routine.

3. **Thread Termination**
   - Function: `pthread_exit`
   - Description: Terminates the thread explicitly.
   - State: Thread resources are cleaned up.

4. **Thread Joining**
   - Function: `pthread_join`
   - Description: Waits for a thread to terminate.
   - State: Main thread blocks until the specified thread finishes.

5. **Thread Detachment**
   - Function: `pthread_detach`
   - Description: Marks a thread as detached, allowing it to run independently.
   - State: Resources are automatically released upon termination.

## Synchronization Mechanisms

1. **Mutex (Mutual Exclusion)**
   - Functions: `pthread_mutex_lock`, `pthread_mutex_unlock`
   - Description: Ensures that only one thread accesses a critical section at a time.

2. **Condition Variables**
   - Functions: `pthread_cond_wait`, `pthread_cond_signal`
   - Description: Allows threads to wait for specific conditions to be met.

## Example Workflow

1. **Create a Thread**
   ```c
   pthread_t thread;
   pthread_create(&thread, NULL, thread_function, NULL);
   ```

2. **Synchronize Threads**
   ```c
   pthread_mutex_lock(&mutex);
   // Critical section
   pthread_mutex_unlock(&mutex);
   ```

3. **Join or Detach Threads**
   ```c
   pthread_join(thread, NULL); // Wait for thread to finish
   pthread_detach(thread);    // Detach thread
   ```

## Visual Representation

```plaintext
+-------------------+
| Main Thread       |
+-------------------+
         |
         v
+-------------------+
| pthread_create    |
+-------------------+
         |
         v
+-------------------+
| New Thread        |
+-------------------+
         |
         v
+-------------------+
| Thread Execution  |
+-------------------+
         |
         v
+-------------------+
| pthread_join      |
+-------------------+
```

## Summary
This schema outlines the lifecycle of threads, key functions, and synchronization mechanisms in pthreads. Use this as a reference to understand and implement multithreading in C effectively.