**Name** : Insyirah Binti Ahmad Mashuri
**Student ID**   : 2022697784
**Group**        : M3CS2554A

#BSD Sockets API

## WHAT IS BSD Sockets API ?

--> The BSD (Berkeley Software Distribution) socket API is a set of system calls and library functions for networking applications in Unix-like operating systems. It originated in the BSD Unix operating system and has since been widely adopted by other Unix-like systems, including Linux. The BSD socket API provides an interface for creating, configuring, and managing network sockets, which are endpoints for communication between processes across a network. It supports both connection-oriented (e.g., TCP) and connectionless (e.g., UDP) communication protocols.

```C
// programming  
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

void error(const char *msg) {
    perror(msg);
    exit(0);
}

int main(int argc, char *argv[]) {
    int sockfd, portno, n;
    struct sockaddr_in serv_addr;
    struct hostent *server;

    char buffer[256];
    if (argc < 3) {
        fprintf(stderr,"usage %s hostname port\n", argv[0]);
        exit(0);
    }

    portno = atoi(argv[2]);
    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0)
        error("ERROR opening socket");

    server = gethostbyname(argv[1]);
    if (server == NULL) {
        fprintf(stderr,"ERROR, no such host\n");
        exit(0);
    }

    bzero((char *) &serv_addr, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    bcopy((char *)server->h_addr,
          (char *)&serv_addr.sin_addr.s_addr,
          server->h_length);
    serv_addr.sin_port = htons(portno);

    if (connect(sockfd,(struct sockaddr *) &serv_addr,sizeof(serv_addr)) < 0)
        error("ERROR connecting");

    printf("Please enter the message: ");
    bzero(buffer,256);
    fgets(buffer,255,stdin);

    n = write(sockfd,buffer,strlen(buffer));
    if (n < 0)
        error("ERROR writing to socket");

    bzero(buffer,256);
    n = read(sockfd,buffer,255);
    if (n < 0)
        error("ERROR reading from socket");

    printf("%s\n",buffer);
    close(sockfd);
    return 0;
}
