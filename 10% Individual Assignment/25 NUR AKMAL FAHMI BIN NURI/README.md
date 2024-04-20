`NUR AKMAL FAHMI BIN NURI | 2022608054 | CDCS2554A | PREPARED FOR SIR SHAHADAN SAAD`
___
# TITLE : Server TCP.c Code Using Python (Socket Programming)
## What is Server?
* Server is a `computer program` or `equipment` that serves another program and its user. In other word, it is called as a client.
* In the client-server programming model, a server program `receives` requests from client programs and `responds` to them.

## What is TCP?
* TCP also known as `Transmission Control Protocol`.
* TCP located at the `Transport Layer` in the OSI Model.
* TCP also is a `communications standard` that allows computer application programs to communicate with one another computing devices over a network.
* TCP is designed to send the `packets` across networks and ensure the packets deliveries and arrivals successfulness.

## What is Socket Programming?
* Socket Programming is a `communication connection point` that user can be name and address in a network.
* The socket **API** (Application Programming Interface) are used to send messages through a network.
* An **easy-to-use** and `reliable` API for Python is available, and it maps straight to the system calls.

## Client-Server TCP.c Socket Programming in Python
### Diagram below shows how client-server TCP.c in Python works :
## ![client-server tcp](https://github.com/addff/2403-ITT440/assets/166005313/15cb3331-8bf6-4aa6-91e3-54908721e603)

## Python Sockets
1. `socket`
2. `bind`
3. `listen`
4. `connect, connect_ex`
5. `accept`
6. `send, recv`
7. `close`

## Server Code
Based on the diagram below, the server bind the socket to port 8888, listen for incoming connection and send a message back when connection is initiated :-

![Screenshot (98)](https://github.com/addff/2403-ITT440/assets/166005313/1004017e-397f-4d30-b02b-9435fca94da2)

## Client Code
Based on the diagram given, the client will create a socket and initiate a connection with the server and print out a response from the server :-
## Output
## Video
