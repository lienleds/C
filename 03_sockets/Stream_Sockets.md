# Stream Sockets (SOCK_STREAM)

Stream sockets, also known as SOCK_STREAM, are one of the most commonly used types of sockets in network programming. They provide reliable, connection-oriented communication between two endpoints. This makes them ideal for applications where data integrity and order are critical, such as web servers, file transfers, and messaging systems.

## Key Features

1. **Reliability**:
   - Stream sockets use the Transmission Control Protocol (TCP) to ensure that data is delivered reliably and in the correct order.
   - TCP handles retransmissions in case of packet loss, ensuring that no data is lost during transmission.

2. **Connection-Oriented**:
   - A connection must be established between the client and server before data can be exchanged.
   - This connection is maintained throughout the communication session.

3. **Byte Stream**:
   - Data is sent as a continuous stream of bytes, without any inherent message boundaries.
   - Applications must define their own protocols to interpret the data.

## How Stream Sockets Work

1. **Server Side**:
   - The server creates a socket and binds it to a specific port.
   - It listens for incoming connection requests from clients.
   - Once a connection is accepted, the server can send and receive data.

2. **Client Side**:
   - The client creates a socket and connects to the server's IP address and port.
   - Once the connection is established, the client can send and receive data.

## Example: Stream Socket Communication

### Server Code

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080

int main() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);
    char buffer[1024] = {0};
    const char *hello = "Hello from server";

    // Create socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    // Bind the socket to the port
    if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    // Listen for incoming connections
    if (listen(server_fd, 3) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }

    // Accept a connection
    if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t *)&addrlen)) < 0) {
        perror("accept");
        exit(EXIT_FAILURE);
    }

    // Read and respond to the client
    read(new_socket, buffer, 1024);
    printf("Message from client: %s\n", buffer);
    send(new_socket, hello, strlen(hello), 0);
    printf("Hello message sent\n");

    close(new_socket);
    close(server_fd);
    return 0;
}
```

### Client Code

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080

int main() {
    int sock = 0;
    struct sockaddr_in serv_addr;
    char buffer[1024] = {0};
    const char *hello = "Hello from client";

    // Create socket
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        printf("Socket creation error\n");
        return -1;
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Convert IPv4 and IPv6 addresses from text to binary form
    if (inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr) <= 0) {
        printf("Invalid address/ Address not supported\n");
        return -1;
    }

    // Connect to the server
    if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
        printf("Connection Failed\n");
        return -1;
    }

    send(sock, hello, strlen(hello), 0);
    printf("Hello message sent\n");
    read(sock, buffer, 1024);
    printf("Message from server: %s\n", buffer);

    close(sock);
    return 0;
}
```

## Handshake Scheme for Stream Sockets

The handshake process is a critical step in establishing a connection between a client and a server using stream sockets. This process ensures that both parties are ready to communicate and agree on the parameters of the connection.

### Steps in the Handshake Process

1. **Server Initialization**:
   - The server creates a socket and binds it to a specific port.
   - It listens for incoming connection requests.

2. **Client Connection Request**:
   - The client creates a socket and sends a connection request to the server.
   - This request includes the client's IP address and port number.

3. **Server Acknowledgment**:
   - The server acknowledges the client's request and prepares to establish the connection.

4. **Connection Establishment**:
   - Once the handshake is complete, the connection is established, and both parties can start exchanging data.

### Example: TCP Handshake

The TCP handshake, also known as the three-way handshake, is a specific implementation of the handshake process for stream sockets. It involves the following steps:

1. **SYN (Synchronize)**:
   - The client sends a SYN packet to the server, indicating its intention to establish a connection.

2. **SYN-ACK (Synchronize-Acknowledge)**:
   - The server responds with a SYN-ACK packet, acknowledging the client's request and indicating its readiness to establish the connection.

3. **ACK (Acknowledge)**:
   - The client sends an ACK packet to the server, confirming the connection.

Once the three-way handshake is complete, the connection is established, and data can be exchanged between the client and server.

### Diagram of the Handshake Process

```plaintext
Client                  Server
  | SYN ----------------> |
  | <---------------- SYN-ACK |
  | ACK ----------------> |
Connection Established
```

## Advantages

- Reliable data transmission.
- Ensures data integrity and order.
- Suitable for long-lived connections.

## Disadvantages

- Higher overhead compared to datagram sockets.
- Requires connection setup and teardown.

## Use Cases

- Web servers and clients.
- File transfer applications.
- Messaging systems.

## Best Practices with Port Numbers

When working with stream sockets, choosing the right port number is crucial for ensuring proper communication and avoiding conflicts. Here are some best practices:

1. **Use Non-Privileged Ports**:
   - Ports below 1024 are considered privileged and require administrative privileges to bind. Use ports above 1024 for user applications.

2. **Avoid Well-Known Ports**:
   - Ports 0-1023 are reserved for well-known services (e.g., HTTP on port 80, HTTPS on port 443). Avoid using these ports to prevent conflicts.

3. **Dynamic/Private Ports**:
   - Ports 49152-65535 are designated as dynamic or private ports. These are often used for temporary connections and are less likely to conflict with other applications.

4. **Document Port Usage**:
   - Clearly document the port numbers used by your application to avoid confusion during deployment and maintenance.

5. **Check for Availability**:
   - Before binding to a port, ensure it is not already in use by another application. Tools like `netstat` or `lsof` can help identify port usage.

## Localhost vs External Host

Understanding the difference between `localhost` and external hosts is essential for configuring and testing network applications.

1. **Localhost**:
   - Refers to the local machine (loopback address).
   - The IP address `127.0.0.1` is reserved for localhost.
   - Used for testing and development purposes.
   - Connections to `localhost` do not leave the local machine, making them faster and more secure for local testing.

2. **External Host**:
   - Refers to any machine other than the local machine.
   - Requires a valid IP address or hostname to connect.
   - Connections to external hosts involve network routing and may pass through firewalls, routers, and other network devices.
   - Used for deploying applications that need to communicate over a network.

### Example

- **Localhost**:
  - A web server running on `localhost` can be accessed using `http://127.0.0.1` or `http://localhost`.
  - This is useful for testing the server locally before making it accessible to others.

- **External Host**:
  - A web server running on an external host can be accessed using its public IP address (e.g., `http://192.168.1.100`) or domain name (e.g., `http://example.com`).
  - This allows other devices on the network or the internet to access the server.

By understanding and applying these best practices, you can ensure that your stream socket applications are robust, secure, and easy to maintain.

Stream sockets are a fundamental concept in network programming. Understanding their features and how to use them is essential for developing robust networked applications.