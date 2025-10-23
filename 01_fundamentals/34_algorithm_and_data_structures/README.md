# Algorithms and Data Structures in C

Algorithms and data structures are fundamental concepts in computer science and programming. They provide efficient ways to organize, manipulate, and process data.

## Common Data Structures

### 1. Arrays
- **Description**: A collection of elements stored in contiguous memory locations.
- **Use Cases**: Storing fixed-size data, implementing other data structures like stacks and queues.

#### Example
```c
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

### 2. Linked Lists
- **Description**: A collection of nodes where each node contains data and a pointer to the next node.
- **Use Cases**: Dynamic memory allocation, implementing stacks and queues.

#### Example
```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

void printList(struct Node* n) {
    while (n != NULL) {
        printf("%d ", n->data);
        n = n->next;
    }
}

int main() {
    struct Node* head = NULL;
    struct Node* second = NULL;
    struct Node* third = NULL;

    head = (struct Node*)malloc(sizeof(struct Node));
    second = (struct Node*)malloc(sizeof(struct Node));
    third = (struct Node*)malloc(sizeof(struct Node));

    head->data = 1;
    head->next = second;

    second->data = 2;
    second->next = third;

    third->data = 3;
    third->next = NULL;

    printList(head);
    return 0;
}
```

### 3. Stacks
- **Description**: A linear data structure that follows the Last In, First Out (LIFO) principle.
- **Use Cases**: Function call management, undo operations.

#### Example
```c
#include <stdio.h>
#define MAX 100

int stack[MAX];
int top = -1;

void push(int value) {
    if (top == MAX - 1) {
        printf("Stack Overflow\n");
    } else {
        stack[++top] = value;
    }
}

int pop() {
    if (top == -1) {
        printf("Stack Underflow\n");
        return -1;
    } else {
        return stack[top--];
    }
}

int main() {
    push(10);
    push(20);
    printf("Popped: %d\n", pop());
    return 0;
}
```

### 4. Queues
- **Description**: A linear data structure that follows the First In, First Out (FIFO) principle.
- **Use Cases**: Task scheduling, buffering.

#### Example
```c
#include <stdio.h>
#define MAX 100

int queue[MAX];
int front = -1, rear = -1;

void enqueue(int value) {
    if (rear == MAX - 1) {
        printf("Queue Overflow\n");
    } else {
        if (front == -1) front = 0;
        queue[++rear] = value;
    }
}

int dequeue() {
    if (front == -1 || front > rear) {
        printf("Queue Underflow\n");
        return -1;
    } else {
        return queue[front++];
    }
}

int main() {
    enqueue(10);
    enqueue(20);
    printf("Dequeued: %d\n", dequeue());
    return 0;
}
```

### 5. Trees
- **Description**: A hierarchical data structure consisting of nodes, with one node as the root and others as children.
- **Use Cases**: Representing hierarchical data, search operations.

#### Example
```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* newNode(int data) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
}

int main() {
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    printf("Root: %d\n", root->data);
    return 0;
}
```

## Common Algorithms

### 1. Sorting
- **Bubble Sort**
- **Quick Sort**
- **Merge Sort**

### 2. Searching
- **Linear Search**
- **Binary Search**

### 3. Graph Algorithms
- **Breadth-First Search (BFS)**
- **Depth-First Search (DFS)**

### 4. Dynamic Programming
- **Knapsack Problem**
- **Fibonacci Sequence**

## Exercises

1. Implement a linked list with insertion and deletion operations.
2. Write a program to perform binary search on a sorted array.
3. Implement a stack using a linked list.
4. Create a binary tree and traverse it using in-order, pre-order, and post-order traversal.
5. Implement a queue using two stacks.

## Additional Resources

- [GeeksforGeeks: Data Structures](https://www.geeksforgeeks.org/data-structures/)
- [Introduction to Algorithms](https://mitpress.mit.edu/9780262046305/introduction-to-algorithms/)
- [C Programming: Data Structures](https://www.tutorialspoint.com/data_structures_algorithms/index.htm)