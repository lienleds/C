# Mailbox IPC in C

A mailbox is a higher-level inter-process communication (IPC) mechanism that allows processes to exchange messages. It is often implemented as a combination of message queues and shared memory, providing a structured way to send and receive messages.

## Key Concepts

1. **Mailbox**:
   - A mailbox is a logical entity that stores messages sent by one process and allows another process to retrieve them.

2. **Message Structure**:
   - Messages typically consist of a header (e.g., type, priority) and a payload (data).

3. **Synchronization**:
   - Mailboxes handle synchronization internally, ensuring that messages are delivered in the correct order.

4. **Blocking and Non-Blocking**:
   - Mailbox operations can be blocking (waiting for a message) or non-blocking (returning immediately if no message is available).

## How Mailboxes Work

1. **Create a Mailbox**:
   - Initialize the mailbox structure and allocate resources.

2. **Send a Message**:
   - Add a message to the mailbox.

3. **Receive a Message**:
   - Retrieve a message from the mailbox.

4. **Destroy the Mailbox**:
   - Clean up resources when the mailbox is no longer needed.

## Example: Mailbox Implementation in C

The following example demonstrates a simple mailbox implementation using a circular buffer.

### Code Example

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

#define MAILBOX_SIZE 5

typedef struct {
    char messages[MAILBOX_SIZE][100];
    int head;
    int tail;
    int count;
    pthread_mutex_t mutex;
    pthread_cond_t not_empty;
    pthread_cond_t not_full;
} Mailbox;

void mailbox_init(Mailbox *mb) {
    mb->head = 0;
    mb->tail = 0;
    mb->count = 0;
    pthread_mutex_init(&mb->mutex, NULL);
    pthread_cond_init(&mb->not_empty, NULL);
    pthread_cond_init(&mb->not_full, NULL);
}

void mailbox_send(Mailbox *mb, const char *message) {
    pthread_mutex_lock(&mb->mutex);

    while (mb->count == MAILBOX_SIZE) {
        pthread_cond_wait(&mb->not_full, &mb->mutex);
    }

    strcpy(mb->messages[mb->tail], message);
    mb->tail = (mb->tail + 1) % MAILBOX_SIZE;
    mb->count++;

    pthread_cond_signal(&mb->not_empty);
    pthread_mutex_unlock(&mb->mutex);
}

void mailbox_receive(Mailbox *mb, char *buffer) {
    pthread_mutex_lock(&mb->mutex);

    while (mb->count == 0) {
        pthread_cond_wait(&mb->not_empty, &mb->mutex);
    }

    strcpy(buffer, mb->messages[mb->head]);
    mb->head = (mb->head + 1) % MAILBOX_SIZE;
    mb->count--;

    pthread_cond_signal(&mb->not_full);
    pthread_mutex_unlock(&mb->mutex);
}

void mailbox_destroy(Mailbox *mb) {
    pthread_mutex_destroy(&mb->mutex);
    pthread_cond_destroy(&mb->not_empty);
    pthread_cond_destroy(&mb->not_full);
}

void *producer(void *arg) {
    Mailbox *mb = (Mailbox *)arg;
    for (int i = 0; i < 10; i++) {
        char message[100];
        sprintf(message, "Message %d", i);
        mailbox_send(mb, message);
        printf("Produced: %s\n", message);
    }
    return NULL;
}

void *consumer(void *arg) {
    Mailbox *mb = (Mailbox *)arg;
    for (int i = 0; i < 10; i++) {
        char message[100];
        mailbox_receive(mb, message);
        printf("Consumed: %s\n", message);
    }
    return NULL;
}

int main() {
    Mailbox mb;
    pthread_t prod, cons;

    mailbox_init(&mb);

    pthread_create(&prod, NULL, producer, &mb);
    pthread_create(&cons, NULL, consumer, &mb);

    pthread_join(prod, NULL);
    pthread_join(cons, NULL);

    mailbox_destroy(&mb);

    return 0;
}
```

## Advantages

- Provides a structured way to exchange messages between processes.
- Handles synchronization internally.
- Supports both blocking and non-blocking operations.

## Disadvantages

- Limited mailbox size.
- Requires additional resources for message storage and synchronization.

## Use Cases

- Communication between threads or processes in real-time systems.
- Task scheduling and job queues.
- Event-driven programming.

Mailboxes are a versatile IPC mechanism that provide a simple and reliable way to exchange messages between processes or threads.