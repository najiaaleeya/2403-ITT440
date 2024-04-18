`MUHAMMAD MINHALKAZIM BIN MOHD SARUSNIZA | 2022484384 | M3CS2554A | ITT440`
# Pass Multiple Random Number using TCP Port

## Socket API Overview
Python’s socket module provides an interface to the <a href="https://en.wikipedia.org/wiki/Berkeley_sockets" target= "blank"> Berkeley sockets API</a>. The primary socket API functions and methods that will be used are:
* `socket()`
* `.bind()`
* `.listen()`
* `.accept()`
* `.connect()`
* `.connect_ex()`
* `.send()`
* `.recv()`
* `.close()`

## TCP Sockets
To better understand this, check out the sequences of socket API calls and data flow for TCP:
<p align="center">
    <img src="https://files.realpython.com/media/sockets-tcp-flow.1da426797e37.jpg" alt="drawing" width="500"/>
</p>

*<p align="center"><a href="https://idiotdeveloper.com/file-transfer-using-tcp-socket-in-python3/" target= "blank">TCP Socket Flow</a></p>*

As it has been showned in the diagram, on the right side is the **client** while the left-hand column represents the **server**. It starts on the top left side column, the API calls so that the server can start to set up a "listening" socket:
* `socket()`
* `.bind()`
* `.listen()`
* `.accept()`

The server **listens** for connections from clients by calling `.listen()`. When a client connects, the server uses `.accept()` to **accept** the connection.

The client calls `.connect()` to establish a connection to the server and initiate the **three-way handshake**. It is important because it ensures that both sides of the connection are reachable in the network. In simpler terms, the client can reach the server and vice-versa. 

Once the connection is established, the client and server use `.send()` and `.recv()` where the **data exchange** happens between both sides. Lastly, the client and server close their respective sockets to end the connection. 
## How to code the Server
```python 
import socket 
import random 

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = socket.gethostname()
port = 27679

try:
    server_socket.bind((host, port))
except socket.error as e:
    print(f"Error: {e}")
    server_socket.close()
    exit(1)
    
server_socket.listen(1)
print("Server listening on {}:{}". format(host, port))

try:
    while True:
        client_socket, addr = server_socket.accept()
        print("Got a connection from {}", format(addr))
        
        random_numbers = [random.randint(1,100) for _ in range(10)]
        number_str = ",".join(str(num) for num in random_numbers)
        
        try:
            client_socket.send(number_str.encode('utf-8'))
        except ssocket.error as e:
            print(f"Error sending data: {e}")

        client_socket.close()
    
except KeyboardInterrupt:
    print("Server terminated by user.")
```

In the above code, we created a **socket instance** for the server. You can see that `socket.AF_INET` defines the address family that this socket can accept – **only IPv4 addresses**. Also, `socket.SOCK_STREAM` defines that the socket accepts only **TCP (Transmission Control Protocol)** connections.

This line of code, `host = socket.gethostname()`, will get the **host name** of the current system under which the Python interpreter is executed. Also, to set the **port number** that the server will listen on by assign `port = 27679`.

The `.bind()` method is used to **associate the socket** with a specific network interface and port number which is `try: server_socket.bind((host, port))`. The values passed to `.bind()` depend on the **address family** of the socket. In this coding, it use `socket.AF_INET` (IPv4). So it expects a two-tuple: **(host, port)**. 

If another process is already bound to this host or port, it will raise a `socket.error` **exception**. `except socket.error as e: print(f"Error: {e}")` **catches** the `socket.error` exception and prints the error message. Then, it **close the socket** if there was an error binding it, `server_socket.close()`, and **exit the program** with a status code of 1, indicating an error occured, `exit(1)`.

`server_socket.listen(1)` puts the server socket in **passive mode**, where it waits for the client to approach the server to make a connection. The argument `1` is the **maximum** number of queued connections. The `.listen()` method has a **backlog parameter**. It specifies the number of **unaccepted connections** that the system will allow before refusing new connections. `print("Server listening on {}:{}". format(host, port))`, this line prints a message indicating that the server is listening.

The `.accept()` method **blocks execution** and waits for an incoming connection. `while True: client_socket, addr = server_socket.accept()` starts infinite loop where the server waits to **accepts** a connection from a client. And if the connection is established, it will **prints** a message, `print("Got a connection from {}", format(addr))`.

This line of code, `random_numbers = [random.randint(1,100) for _ in range(10)]`, will generatess a list of 10 **random numbers** between 1 and 100. Then, to converts the list of numbers into a **comma-separated** string, use `number_str = ",".join(str(num) for num in random_numbers)`. 

After that, it needs to be ***<a href="https://docs.python.org/3/library/socket.html#socket.socket.send" target= "blank">send</a>*** to the client by using this line of code, `try: client_socket.send(number_str.encode('utf-8'))`. If the fails to send, it will print an **error messages**, `except ssocket.error as e: print(f"Error sending data: {e}")`. Then, the client **close** its socket by `client_socket.close()`. Lastly, if the user **interrupts** the program (e.g., by pressing Ctrl+C), it prints a message indicating that the server was terminated by the user, `except KeyboardInterrupt: print("Server terminated by user.")`.
## How to code the Client
```python 
import socket

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = socket.gethostname()
port = 27679

try:
    client_socket.connect((host, port))
except socket.error as e:
    print(f"Error connecting to the server: {e}")
    client_socket.close()
    exit(1)

received_data = client_socket.recv(1024).decode('utf-8')

number_list = received_data.split(',')
```

In the above code, we created a **socket instance** for the server. You can see that `socket.AF_INET` defines the address family that this socket can accept – **only IPv4 addresses**. Also, `socket.SOCK_STREAM` defines that the socket accepts only **TCP (Transmission Control Protocol)** connections.

This line of code, `host = socket.gethostname()`, will get the **host name** of the current system under which the Python interpreter is executed. Also, to set the **port number** that the server will listen on by assign `port = 27679`.

The client have to **connect** to the server at the given host and port by using the `.connect()` system. The connect() system call connects the socket referred to by the file descriptor sockfd to the address specified by **addr**, `try: client_socket.connect((host, port))`. Server’s address and port is specified in addr. But if the connections **fails**, it will prompt an error messages, `except socket.error as e: print(f"Error connecting to the server: {e}")`. Then, the client socket will **close**, `client_socket.close()`.

`received_data = client_socket.recv(1024).decode('utf-8')`, this line **receives** data from the server. The `.recv()` method takes one argument that specifies the maximum amount of data to be **received** at once (1024 bytes in this case). The received data is then decoded from bytes to a string using **UTF-8 encoding**. 

`number_list = received_data.split(',')`, this line **splits** the received string into a list of numbers using the comma as a separator.

## Output

<p align="center">
    <img src="https://lh3.googleusercontent.com/pw/AP1GczMcUwm0QAflG2bBdW-ZEJ5Wzyj-VH-DoVtL96khHwxxYYGpBMSJKAmiTMNixWZ10YROCBuveXS-rgrE9cn5wrBvnv2fG_kXvzA4SXqW2vdaCLYdYiXQminTOrlvi_yUjgI0rGrprGXBgT-PE3XLoFWITxY_JqiBGfFJ7RnUqqXwNebTByBmA5k91VMZV4bWFpwiyBEOjrSfOVWgssTIW2jFKpicTwQLkr3PJSbdFW6oSM3eCnqPEJ4FH8oMCPUAa0C9RrznyZMslVGZCyqs7RvS88KPGzm_snolxIv54-2SBLFG6NweBupZ0w6ROi-ybJXbLxzvXuvRNYwWjdXacqByF3glARtkS1u9Nf9wO7B2qFfVbyw5xVbQnry1LxkF8kNwxCGqI3c_Lo4Lu3q4QGrCa-S3lP6WlcFiVq8QOGBS0POo80D3hwW2a4RZ8L1KmS4UtsWPayogfPADkgBTx0CXfQE-Sy1xqY-psqsrQhQ7Vfh2GtjcZWWj3Zn2LEWpX15MFXSDg9APOtCW2NGLhwQLUaP6FXrEzSS4Zz1lwymqbI5KBBwkehGqDh6smDuK_YMIou7BAKyndj04i57F_DODVZCgk0q61GqvnuYETiEdBQQZLG4xxkga_XS6-nsQB3gqTBxhEH0oRmBBEIAEn1w2tLeDWKWZHVHvx-CPiMLwH6nZpvAAg8vkVZefou64g5ff0bOsDHmz_Z9Ad3btvn4oT4cuer6WWcS9qLc-q2sp4vWAiHRpULm4rL5KNKf_Npavk1gjE5G0gaMAubqjLYOCIt0qzOFSk7Znl264ggrI9IlM-9XsK6VsVkyaNp0iZ6KhPF-0zLQBCW61lYPozzcm2Bi82Qr0vC4I5J2PseaebBQ_4DP0fr-baOArG6XQ6gytvwcXDOFVjbVH68XVL4dw2xX4YqspXjANCkpdrGt80gOrUTk5IrOoSh7LgA-KXCgBT9S47OcJt_tkbTGCDNWpvfZe-NVjIf75EfRjnSdYjYS-QdhW-3mSA0yyPRKqCw=w376-h69-s-no-gm?authuser=2" alt="drawing" width="500"/>
</p>

*<p align="center">server.py</p>*

<p align="center">
    <img src="https://lh3.googleusercontent.com/pw/AP1GczNNE_CpQdxh-2bPm0EUgkHfRtxH8RCiOX7YY9sHt5JT5pHbvP5Sy4-6bsahY-83aegzPfYpqcRl601So0jshPJaglnYb5IEkfwKjFqRTy1hCr-baD8H5xWlokOBnb4lHhN93zY1GuWbrbC8LQTHhtM4GQL71IhZBlFg7kIw7YFhb2zKpmJvEPEvBdW2oldWWVNJX8D1oeK0y7ChOcLIkNGJpZo8Kqzx0McTc4u6xNDmYXSuX8r05d7NEltSkegBbXF6j-UC2GPoTz7STyA4_0-MK1lYv8fL6rN33WJX_0Se0pjNy7VQ0GXcOD0zfTfzuKljH2w5FOFkoQJ4SufLthb1RH0Kh8IIwkXGP1BKriZ9Lze_bV_PBk_VHgJkXfE9FLklZNoQJTazl_CZY0-hNUzIeq8YfrsSLRbARNJaZOsdSZlrFw9baMctMGVaApInzW3ilP6oA8I_fkvdf9wt6r9rdC3Gx7gfCLRiywxMyqVz5oAbHZfxqYiHWdny4ArFgU6Ur4R-a3fAfOtXC30MaIBNR5__5iQHv5iqPW60IfRdLNPbOgprBLsiUNq3aTxJ_8ODZy45sjWYok4oP3HKQzsRslsaVoirf92kUVG0tbld6ldB-jSNu_QTqEJ9WrpH8ax4udAGNBdv6U313yWLUC74boSlrnTsdzYoIPa6Ml2Xgl5Uov5-cIwCfWwnofWekOAnbwkqZrQ20V3b8qZncniZd5FMPwVqk0OH0H0b2VfgO54qiz1hvOv2L8K9aikqKN9uQfA7AwmKNlGxplheihSrnuEqUynWQ7R1UzTcq1Ji9vEJcwIqOhMj8nYZiXyHPgWpArHFUIH0VkUXEh9NHFqpxwLQuPoQQRYevs3VGwrUBmxdhHU61DJTQK7BoYtIERqg6sGmiMLWPptaC-UoYQTKgCHXwY9qeMBhj9ZYiqr2gaJNKHZlcV8yZ-0IvWyD68uZeiyUU6frmaIhaji6XmvHLI3whhOvUbX3I5wB0Vw6kGSBlBSjWnqGCxmxIfWudg=w650-h29-s-no-gm?authuser=2"alt="drawing" width="8000"/>
</p>

*<p align="center">client.py</p>*

## Video
<p align="center">
    <a href="https://youtu.be/9UL6xB5qFkI" target= "blank"><img src="https://lh3.googleusercontent.com/pw/AP1GczODu2oGm2hS3xIHRttIhQA548bfuYM9Rr3y3PLJN9gCa-Q6syJMM5IVKSWzJwxwME9l20m_lGq_ReYmxlCt1oP16sc-_KtV4EqXtw8_2JfP-sG4uk1zJvbanIE4V91rcr-_iiKluBNPPGxvF1slVRcletRO6rw8HJCSFLzT-LpOLc3FadfNQ8ogV_qm3vq_MyZ89vxBbGQvhs8iT9cmV8Ki-9tOHazvaNRpeHvjiX6yodBHf1xeN2I2erpz0fqGJl9uAhvwd9Kl9CvVDV6QcXoV6wfAarUd_VFIQvIencglJKAGSckBM2X_DkSozKuWaXi8w0nCN-P_8B9zDhhE9bqlr-F-GdLS6km2DL2bRU4Pk__MwuCFhbJMkQG0o5soBKphVpvEuckGGPl3rrhjWdqbg8K-xaPtDGDxVDXZcJlReKWg49RiUY6vMn3KvLNe-s8K6Vqcl-Gff-bAMEcD8O8XRoD1qyN7s24mWXTsluw3Gr6G6to67tCos8T8vOrL6HdbD6v9veBy3tpqa8VONiKGxT9EBU_Qyuh1m9Wj6_C4yAq2b5GntYG5q6v1ZuQe9KRSmvkcyeD1ASyEsYLXVuYncItamfDb1HRgIUpGe2n1OZJAulTFqq45uvjNG5ijrrXXSi83t4KpADmpjhHf_8xYB2hIDUGK4npbFVfFHsbshXFWOMojY7vYIXjUtdkk3oDyZbfhOVRzbBe-2f_ODQEEmz1TvFmBWPvHDj-ZjzKLHp-09uc1bvXg1K66l-T9x-FG9T9fmSJ6tPFO_5YW6EPICz7Ck8LXIOxFTwxAbRwL0AWpKGjsbhihj1Ca4C7wt0L60UAKyMfSCX9NCx94uRONpBPZvWHN9AZtKWc9CbVUCNKhwXuNlO_wSuEcOeV7qEls2SlNxWMBzl9pwS_cg8S457u9jp7wkq_iHcHJTDW6j-Oa8RG2vCfkF5qXH_b11E_pT8huCKv0_axicWbDL7To_Jr9Exos0VQzpCM9kfDPzlXapltYHPsg4iMN2kG7BA=w1590-h894-s-no-gm?authuser=2"/>
    </a>
</p>

