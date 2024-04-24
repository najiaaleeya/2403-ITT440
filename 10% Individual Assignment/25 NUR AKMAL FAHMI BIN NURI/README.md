`NUR AKMAL FAHMI BIN NURI | 2022608054 | CDCS2554A | ITT440 | PREPARED FOR SIR SHAHADAN SAAD`
___
# TITLE : Server TCP Code Using Python (Socket Programming)
## What is Server?
* Server is a *computer program* or *equipment* that serves another program and its user. In other word, it is called as a client.
* In the client-server programming model, a server program *receives* requests from client programs and *responds* to them.

## What is TCP?
* TCP also known as *Transmission Control Protocol*.
* TCP located at the *Transport Layer* in the OSI Model.
* TCP also is a *communications standard* that allows computer application programs to communicate with one another computing devices over a network.
* TCP is designed to send the *packets* across networks and ensure the packets deliveries and arrivals successfulness.

## TCP Header
![Screenshot (123)](https://github.com/addff/2403-ITT440/assets/166005313/58ebf559-ec67-41c9-8b9a-b95b37931c30)

## What is Socket Programming?
* Socket Programming is a *communication connection point* that user can be name and address in a network.
* The socket *API* (Application Programming Interface) are used to send messages through a network.
* An *easy-to-use* and *reliable* API for Python is available, and it maps straight to the system calls.

## Client-Server TCP.c Socket Programming in Python
### Diagram below shows how client-server TCP.c in Python works :
## ![client-server tcp](https://github.com/addff/2403-ITT440/assets/166005313/15cb3331-8bf6-4aa6-91e3-54908721e603)

## Python Sockets
1. `socket()` = Creates a new socket.
2. `bind()` = Associates the socket to a specific address and port.
3. `listen()` = Starts listening for incoming connections on socket.
4. `connect()` = Establishes a connection to a remote server.
5. `accept()` = Accepts a connection from a client and returns a new socket for communication.
6. `send()` = Sends data through the socket.
7. `recv()` = Receives data from the socket.
8. `close()` = Closes the socket connection.

## Codes (Both client and server code are required to run this programme)
### Server Code
Based on the diagram below, the server bind the socket to port 27679, listen for incoming connection and send a message back when connection is initiated :-
![Screenshot (119)](https://github.com/addff/2403-ITT440/assets/166005313/4d86fe45-6ab0-4cfc-b86e-7e85cf9d86e7)

### Client Code
Based on the diagram given, the client will create a socket and initiate a connection with the server and print out a response from the server :-
![Screenshot (121)](https://github.com/addff/2403-ITT440/assets/166005313/4ae6ef88-4f01-4743-8529-4bee55b7fefc)

## Output
### Server Output
![Screenshot (120)](https://github.com/addff/2403-ITT440/assets/166005313/520479ea-376e-4b2e-aee3-ff7b47a52871)

### Client Output
![Screenshot (122)](https://github.com/addff/2403-ITT440/assets/166005313/06e39ce7-b0dd-4df7-97ee-49b8ce649a17)

## Video
