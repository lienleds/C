# Message Queues in C

Message queues are a method of inter-process communication (IPC) that allow processes to exchange data in the form of messages. Unlike shared memory, message queues provide a structured way to send and receive messages, ensuring data integrity and synchronization.

## Key Concepts

1. **Message Queue**:
   - A message queue is a data structure that stores messages in a FIFO (First In, First Out) order.

2. **System Calls**:
   - Message queues in C are implemented using system calls like `msgget`, `msgsnd`, `msgrcv`, and `msgctl`.

3. **Message Structure**:
   - Each message consists of a type (an integer) and a data payload.

4. **Synchronization**:
   - Message queues handle synchronization internally, ensuring that messages are delivered in the correct order.

## How Message Queues Work

1. **Create a Message Queue**:
   - Use `msgget` to create a new message queue or access an existing one.

2. **Send a Message**:
   - Use `msgsnd` to send a message to the queue.

3. **Receive a Message**:
   - Use `msgrcv` to receive a message from the queue.

4. **Control the Queue**:
   - Use `msgctl` to perform control operations like deleting the queue.

## Example: Message Queue in C

The following example demonstrates how two processes can communicate using a message queue.

### Code Example

#### Sender Process

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MSG_KEY 0x1234

struct message {
    long type;
    char text[100];
};

int main() {
    int msgid;
    struct message msg;

    // Create message queue
    msgid = msgget(MSG_KEY, IPC_CREAT | 0666);
    if (msgid < 0) {
        perror("msgget");
        exit(1);
    }

    // Prepare the message
    msg.type = 1;
    strcpy(msg.text, "Hello, Message Queue!");

    // Send the message
    if (msgsnd(msgid, &msg, sizeof(msg.text), 0) < 0) {
        perror("msgsnd");
        exit(1);
    }

    printf("Message sent: %s\n", msg.text);

    return 0;
}
```

#### Receiver Process

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MSG_KEY 0x1234

struct message {
    long type;
    char text[100];
};

int main() {
    int msgid;
    struct message msg;

    // Access the message queue
    msgid = msgget(MSG_KEY, 0666);
    if (msgid < 0) {
        perror("msgget");
        exit(1);
    }

    // Receive the message
    if (msgrcv(msgid, &msg, sizeof(msg.text), 1, 0) < 0) {
        perror("msgrcv");
        exit(1);
    }

    printf("Message received: %s\n", msg.text);

    return 0;
}
```

## Advantages

- Provides a structured way to exchange data between processes.
- Handles synchronization internally.
- Suitable for communication between unrelated processes.

## Disadvantages

- Limited message size.
- Requires system resources to maintain the queue.
- Slower than shared memory due to message copying.

## Use Cases

- Communication between processes in distributed systems.
- Logging and event notification systems.
- Task scheduling and job queues.

Message queues are a versatile IPC mechanism that provide a simple and reliable way to exchange data between processes.