# CREATE BASIC WEB SERVER USING C SOCKET AND HTML
_______
This C code implements a basic web server using sockets in Unix.

## STEP BY STEP METHOD

Before you begin, please make sure you alreadu have the necessary setup:
* VMWare Workstation: You can download and install VMWare Workstation [here](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html).

* FreeBSD Image: Download the FreeBSD image [here](https://www.freebsd.org/where/) and run it on VMWare Workstation.

* MobaXterm: You can download and install MobaXterm [here](https://mobaxterm.mobatek.net/download.html).

## Function: `Header`
These headers are included for various functionalities required by the C program:

- `stdio.h`: This header provides standard input/output functionality. It includes functions like `printf` and `fopen` for reading and writing files.

- `stdlib.h`: This header provides general utilities and memory management functions such as memory allocation (`malloc`, `calloc`, `realloc`) and process control (`exit`, `system`).

- `string.h`: This header provides string manipulation functions like `strcpy`, `strcat`, `strlen`, etc.

- `unistd.h`: This header provides access to the POSIX operating system API. It includes various function declarations like `close`, `read`, and `write`.

- `arpa/inet.h`: This header provides functions for handling internet addresses, including conversions between network and presentation formats (`inet_ntoa`, `inet_addr`).

- `sys/types.h` and `sys/socket.h`: These headers provide the necessary data structures and function declarations for socket programming.

- `netinet/in.h`: This header provides the data structures required for handling internet addresses, specifically the `struct sockaddr_in` structure used for IPv4 socket addresses.

Below is the necessary C code to be included :
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#define PORT 8080
#define BUFFER_SIZE 1024
#define HTML_FILE "aqil/design.html"
```

## Function: `handle_request`

This function is responsible for handling incoming HTTP requests from clients. It reads the content of a static HTML file specified by the `HTML_FILE` constant and sends it as a response to the client. If the HTML file cannot be opened, it prints an error message and exits the program.

### Parameters:
- `client_socket`: Integer representing the socket descriptor for the client connection.

### Steps:
1. Open the HTML file specified by `HTML_FILE` in read mode.
2. Check if the file was opened successfully. If not, print an error message and exit the program.
3. Prepare the HTTP response headers with status code 200 (OK) and content type as text/html.
4. Send the HTTP response headers to the client using the `send` function.
5. Read the content of the HTML file in chunks of size `BUFFER_SIZE` and send each chunk to the client using the `send` function.
6. Close the HTML file after sending its content to the client.

Below is the necessary C code to be included :

```c
void handle_request(int client_socket) {
    FILE *html_file = fopen(HTML_FILE, "r");
    if (html_file == NULL) {
        perror("Failed to open HTML file");
        exit(EXIT_FAILURE);
    }

    char buffer[BUFFER_SIZE];
    size_t bytes_read;

    // Prepare HTTP response headers
    const char *http_response = "HTTP/1.1 200 OK\r\n"
                                "Content-Type: text/html\r\n"
                                "\r\n";

    // Send HTTP response headers
    send(client_socket, http_response, strlen(http_response), 0);

    // Read content of HTML file and send it to client
    while ((bytes_read = fread(buffer, 1, sizeof(buffer), html_file)) > 0) {
        send(client_socket, buffer, bytes_read, 0);
    }

    fclose(html_file);
}
```
## Function: `main`

This is the main function of the HTTP server. It performs the following tasks:

1. **Socket Creation**: Creates a socket using the `socket` function, specifying the address family (`AF_INET` for IPv4), socket type (`SOCK_STREAM` for TCP), and protocol (0 for default protocol).
2. **Server Address Initialization**: Initializes the server address structure (`server_addr`) with the IP address (set to `INADDR_ANY` to listen on all available interfaces) and port number (`PORT`).
3. **Binding**: Binds the socket to the server address using the `bind` function.
4. **Listening**: Listens for incoming connections using the `listen` function.
5. **Accepting Connections**: Enters a loop to accept incoming connections using the `accept` function. Upon accepting a connection, it prints the client's IP address and port.
6. **Handling Requests**: Calls the `handle_request` function to handle the client's HTTP request.
7. **Closing Connections**: Closes the client socket after handling the request.
8. **Cleanup**: Closes the server socket before exiting.

Below is the necessary C code to be included :

```c
int main() {
    int server_socket, client_socket;
    struct sockaddr_in server_addr, client_addr;
    socklen_t addr_len = sizeof(struct sockaddr_in);

    // Create socket
    if ((server_socket = socket(AF_INET, SOCK_STREAM, 0)) == -1) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }

    // Initialize server address struct
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;
    server_addr.sin_port = htons(PORT);

    // Bind socket to address and port
    if (bind(server_socket, (struct sockaddr *)&server_addr, sizeof(server_addr)) == -1) {
        perror("Binding failed");
        exit(EXIT_FAILURE);
    }

    // Listen for incoming connections
    if (listen(server_socket, 10) == -1) {
        perror("Listening failed");
        exit(EXIT_FAILURE);
    }

    printf("Server listening on port %d...\n", PORT);

    // Accept incoming connections and handle requests
    while (1) {
        if ((client_socket = accept(server_socket, (struct sockaddr *)&client_addr, &addr_len)) < 0) {
            perror("Acceptance failed");
            exit(EXIT_FAILURE);
        }

        printf("Connection accepted from %s:%d\n", inet_ntoa(client_addr.sin_addr), ntohs(client_addr.sin_port));

        // Handle request
        handle_request(client_socket);

        close(client_socket);
    }

    close(server_socket);
    return 0;
}




