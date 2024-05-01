**Student Name** : Tengku Zafran Shah bin Tengku Iskandar Zulkarnain

**Student ID**   : 2022842268

**Group**        : M3CS2554A

**Title**        : ITT440 10% Individual Assignment

**Lecturer**     : Sir Shahadan Saad

# Socket Programming in C VS Python

## What is Socket Programming ?

### Definition 

Socket programming is a method of establishing a brief connection between two existing nodes to communicate with each other. The two nodes are commonly known as **Client** and **Server**. The way of communicating is usually one node listens on a particular port with assigned IP address, while the other node reachs out to form a brief connection. The connection is commonly made for accessing resources from the other node such as files, songs, videos, or some other services. For more detailed informations about __Client__ and __Server__ are as follows:

`Client` --> The client is what sends a request to that server socket, and waits for a response.

`Server` --> Server's sole purpose is to do as what its name implies - serve its **Client**.

_The diagram below showing how the `Client-Server` interact to establish connection_ :


![How client-server works](https://github.com/addff/2403-ITT440/assets/166004983/8a4d080a-1999-4b43-91c5-4552913cbb9a)

* `socket()` --> Creating a new socket.
* `bind()` --> Binding the socket to a specific port and an IP address so that socket can communicate.
* `listen()` --> Waiting for feedback from the other end for incoming connection request.
* `accept()` --> Accepting a connection from client and returning a brand new socket to start communicating.
* `connect()` --> Establishing a connection to a remote and private server.
* `write()` --> Sending data that was requested through the socket created.
* `read()` --> Receiving data that was sended from the socket.
* `close()` --> Ending the session by closing the socket connection.

There are various programming languages that can be used to code socket programming and the most popular ones are __C__ and __Python__. In this experiment on finding out which language is better for socket programming, a simple `Client-Server` program will be made to print message if connection is established.

## Socket Programming in C

### Server :

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 27679

int main() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int addrlen = sizeof(address);

    // Creating socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    // Forcefully attaching socket to the port 27679
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // Forcefully attaching socket to the port 27679
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address))<0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    if (listen(server_fd, 5) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }

    while(1) {
        // Accept connection from client
        if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen))<0) {
            perror("accept");
            exit(EXIT_FAILURE);
        }

        printf("Got connection from %s\n", inet_ntoa(address.sin_addr));

        // Send a thank you message to the client
        char *message = "Thank you for establishing connection";
        send(new_socket, message, strlen(message), 0);

        // Close the connection
        close(new_socket);
    }

    return 0;
}
```

### Client :

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 27679

int main() {
    int sock = 0, valread;
    struct sockaddr_in serv_addr;
    char *message = "Hello from client";
    char buffer[1024] = {0};

    // Create socket
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        printf("\n Socket creation error \n");
        return -1;
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Convert IPv4 and IPv6 addresses from text to binary form
    if(inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr)<=0) {
        printf("\nInvalid address/ Address not supported \n");
        return -1;
    }

    // Connect to server
    if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
        printf("\nConnection Failed \n");
        return -1;
    }

    // Receive data from server and print it
    valread = read(sock, buffer, 1024);
    printf("%s\n", buffer);

    // Close the connection
    close(sock);

    return 0;
}
```

### Compiling :

 ```C
 gcc client.c -o client
 gcc server.c -o server
 ```

### Output :


 
 ## Socket Programming in Python

 ### Server :

 ```Python
import socket

# Create a socket object
s = socket.socket()

# Define the port on which you want to connect
port = 27679

# Bind to the port
s.bind(('localhost', port))

# Wait for client connection
s.listen(5)

while True:
    # Establish connection with client
    c, addr = s.accept()
    print('Got connection from', addr)

    # Send a thank you message to the client
    c.send('Thank you for establishing connection'.encode())

    # Close the connection
    c.close()
```

 ### Client :

 ```Python
import socket

# Create a socket object
s = socket.socket()

# Define the port on which you want to connect
port = 27679

try:
    # Connect to the server
    s.connect(('localhost', port))

    # Receive data from server and print it
    print(s.recv(1024).decode())

    # Close the connection
    s.close()
except ConnectionRefusedError:
    print("Connection refused. Make sure the server is running.")

 ```

 ### Output :

 The output in server terminal is as follows:

 ![Screenshot 2024-05-01 213443](https://github.com/addff/2403-ITT440/assets/166004983/5492f40a-53d6-4b05-b1c7-5bdb9838a339)

 * The server will print the IP address and the port that were used to establish connection between client and server.
 * The port will be different if the server code is run again and it will never be the same as before.

 The output in client terminal is as follows:

 ![Screenshot 2024-05-01 213527](https://github.com/addff/2403-ITT440/assets/166004983/019fcf5c-e975-4757-9860-5cb47398ffbe)

 * The client will print out the message if connection is successfully established between client and server.
 
 ## C or Python, Which Language is Better ?

There is no definite answer for above question as different programmers would have different opinion on which language is more suitable for socket programming. Alas, what programmer seek in learning and creating socket programming will differ on which language that they use. At the end of the day, both languages give different exposure and knowledge to its user.

 | Socket Programming with C | Socket Programming with Python |
 | ------------------------- | ------------------------------ |
 | Longer line of codes with detailed commands | Shorter line of codes with simpler commands  |
 | Complex and too detailed for beginner       | Beginner-friendly                            |
 | Good for deeper understanding on the flow of socket programming | Only utilise the surface level of socket programming | 
 

 ## Video

 
