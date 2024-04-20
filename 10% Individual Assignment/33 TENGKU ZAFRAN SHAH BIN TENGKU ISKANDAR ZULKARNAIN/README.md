**Student Name** : Tengku Zafran Shah bin Tengku Iskandar Zulkarnain

**Student ID**   : 2022842268

**Group**        : M3CS2554A

**Title**        : ITT440 10% Individual Assignment

**Lecturer**     : Sir Shahadan Saad

# Socket Programming in C VS Python

## What is Socket Programming ?

### Definition 

Socket programming is a method of establishing a brief connection between two existing nodes to communicate with each other. The two nodes are commonly known as **Client** and **Server**. The way of communicating is usually one node listens on a particular port with assigned IP address, while the other node reachs out to form a brief connection. The connection is commonly made for accessing resources from the other node such as files, songs, videos, or some other services. For more detailed informations about __Client__ and __Server__ are as follows:

`Client` --> 

`Server` --> Server's sole purpose is to do as what its name implies - serve its **Client**.

_The diagram below showing how the `Client-Server` interact to establish connection_ :

<p align="left">
    <img src="https://photos.google.com/photo/AF1QipPkmVQcxzU0mfLw7QwNyBvL2LFbcOd_oOlSNJFm" width="500"/>
</p>

* `socket()` --> Creating a new socket.
* `bind()` --> Binding the socket to a specific port and an IP address so that socket can communicate.
* `listen()` --> Waiting for feedback from the other end for incoming connection request.
* `accept()` --> Accepting a connection from client and returning a brand new socket to start communicating.
* `connect()` --> Establishing a connection to a remote and private server.
* `send()` --> Sending data that was requested through the socket created.
* `recv()` --> Receiving data that was sended from the socket.
* `close()` --> Ending the session by closing the socket connection.

 ### Types of Socket Programming ?

 ## Socket Programming in C

`Client`
```C
// Client side C/C++ program to demonstrate Socket  
// programming  
#include <arpa/inet.h>  
#include <stdio.h>  
#include <string.h>  
#include <sys/socket.h>  
#include <unistd.h>  
#define PORT 8080  
  
int main(int argc, char const* argv[])  
{  
       int sock = 0, valread, client_fd;  
       struct sockaddr_in serv_addr;  
       char* hello = "Hello from client";  
       char buffer[1024] = { 0 };  
       if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {  
               printf("\n Socket creation error \n");  
               return -1;  
       }  
  
       serv_addr.sin_family = AF_INET;  
       serv_addr.sin_port = htons(PORT);  
  
       // Convert IPv4 and IPv6 addresses from text to binary  
       // form  
       if (inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr)  
               <= 0) {  
               printf(  
                       "\nInvalid address/ Address not supported \n");  
               return -1;  
       }  
  
       if ((client_fd  
               = connect(sock, (struct sockaddr*)&serv_addr,  
                               sizeof(serv_addr)))  
               < 0) {  
               printf("\nConnection Failed \n");  
               return -1;  
       }  
       send(sock, hello, strlen(hello), 0);  
       printf("Hello message sent\n");  
       valread = read(sock, buffer, 1024);  
       printf("%s\n", buffer);  
  
       // closing the connected socket  
       close(client_fd);  
       return 0;  
}
```

`Server`
```C
// Server side C/C++ program to demonstrate Socket  
// programming  
#include <netinet/in.h>  
#include <stdio.h>  
#include <stdlib.h>  
#include <string.h>  
#include <sys/socket.h>  
#include <unistd.h>  
#define PORT 8080  
int main(int argc, char const* argv[])  
{  
       int server_fd, new_socket, valread;  
       struct sockaddr_in address;  
       int opt = 1;  
       int addrlen = sizeof(address);  
       char buffer[1024] = { 0 };  
       char* hello = "Hello from server";  
  
       // Creating socket file descriptor  
       if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) < 0) {  
               perror("socket failed");  
               exit(EXIT_FAILURE);  
       }  
  
       // Forcefully attaching socket to port 8080  
       if (setsockopt(server_fd, SOL_SOCKET,  
                               SO_REUSEADDR | SO_REUSEPORT, &opt,  
                               sizeof(opt))) {  
               perror("setsockopt");  
               exit(EXIT_FAILURE);  
       }  
       address.sin_family = AF_INET;  
       address.sin_addr.s_addr = INADDR_ANY;  
       address.sin_port = htons(PORT);  
  
       // Forcefully attaching socket to port 8080  
       if (bind(server_fd, (struct sockaddr*)&address,  
                       sizeof(address))  
               < 0) {  
               perror("bind failed");  
               exit(EXIT_FAILURE);  
       }  
       if (listen(server_fd, 3) < 0) {  
               perror("listen");  
               exit(EXIT_FAILURE);  
       }  
       if ((new_socket  
               = accept(server_fd, (struct sockaddr*)&address,  
                               (socklen_t*)&addrlen))  
               < 0) {  
               perror("accept");  
               exit(EXIT_FAILURE);  
       }  
       valread = read(new_socket, buffer, 1024);  
       printf("%s\n", buffer);  
       send(new_socket, hello, strlen(hello), 0);  
       printf("Hello message sent\n");  
  
       // closing the connected socket  
       close(new_socket);  
       // closing the listening socket  
       shutdown(server_fd, SHUT_RDWR);  
       return 0;  
}
```

 ## Socket Programming in Python

 ## C or Python, Which Language is Better ?

 ## Video

 
