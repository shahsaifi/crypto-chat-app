# Cryptography Coursework Project [chatApp]

---
It is a chat application that demonstrates asymmetric and symmetric encryption.

It is developed with python version `3.9.6` and [requirements.txt](./requirements.txt) contains required libraries.

The server and the client generate public/private keys at runtime and exchange them, then server uses client's public 
key to encrypt a randomoly generated session key that will be shared with the client. 

After this process the client decrypts it with a private key and uses secret to encrypt/decrypt messages using AES in 
Cipher FeedBack (CFB) mode. The server can handle multiple client connections, and it doesn't log the messages keeping clients communication secure.


### Usage

#### To start server:
```bash
➜  python3 server.py -p 9443
[+] Running on host: 127.0.0.1
[+] Running on port: 9443
```

#### To start a client chat session:
it requires three parameters, -s server ip, -p server port number, -u username:
```bash
➜  python3 client.py -s 127.0.0.1 -p 9443 -u sahnawaz
[+] Connected successfully.
[+] Exchanging keys.
[+] Getting public key from the server
[+] Sending public key to server
[+] Exchange completed!
[+] Initial set up had been completed!
[+] Now you can start to exchange messages
```

#### To Terminate `server`, we can issue `TERMINATE` command at `server` console:
```bash
TERMINATE
[+] All connections had been terminated
[+] Server is shut down
```

#### For `client` session termination, we can issue `EXIT` command at `client` console:
```bash
EXIT
# Message at server
[+] sahnawaz left the server.
```
---
## Demo
- install dependent python packages from [requirements.txt](./requirements.txt):
    ```bash
    $ pip install -r requirements.txt
    ```

- starting `server`
    ```bash
    ➜ python3 server.py -p 9443                         
    [+] Running on host: 127.0.0.1
    [+] Running on port: 9443
    ```
- `client-1` joining from other terminal with generating and exchanging keys:
    ```bash
    ➜ python3 client.py -s 127.0.0.1 -p 9443 -u sahnawaz
    [+] Connected successfully.
    [+] Exchanging keys.
    [+] Getting public key from the server
    [+] Sending public key to server
    [+] Exchange completed!
    [+] Initial set up had been completed!
    [+] Now you can start to exchange messages
    ```
  
- key files are written to path for client and server:
    ```bash
    ├── README.md
    ├── client.py
    ├── client_private_key.pem     -----> client private key
    ├── client_public_key.pem      -----> client public key
    ├── requirements.txt
    ├── server.py
    ├── server_private_key.pem    -----> server private key
    └── server_public_key.pem     -----> server public key
    ```
- `client-2` joining from third terminal:
    ```bash
    ➜ python3 client.py -s 127.0.0.1 -p 9443 -u Ira 
    [+] Connected successfully.
    [+] Exchanging keys.
    [+] Getting public key from the server
    [+] Sending public key to server
    [+] Exchange completed!
    [+] Initial set up had been completed!
    [+] Now you can start to exchange messages
    ```
- server side communication info for client-1 (`sahnawaz`) & client-2 (`Ira`):
    ```bash
    [+] New connection. Username: sahnawaz
    [+] Client public key had been received
    [+] Secret key had been sent to the client
    [+] New connection. Username: Ira
    [+] Broadcast message:  New person joined the room. Username: Ira
    [+] Client public key had been received
    [+] Secret key had been sent to the client
    ```
- message exchanges between client-1 & client-2 with server side info:  
    ```bash
    # client-2
    2023-06-25 09:35:24 Ira: Hi
    Hello Ira
  
    # client-1
    Hi
    2023-06-25 09:35:36 sahnawaz: Hello Ira
  
   # server side
  2023-06-25 09:35:24 Mesage exchanged
  2023-06-25 09:35:36 Mesage exchanged
    ```
- session closure and server termination
    ```bash
    # client-2
    EXIT
  
    # client-1
    EXIT
  
   # server side
    [+] Ira left the server.
    [+] sahnawaz left the server.
    TERMINATE
    [+] All connections had been terminated
    [+] Server is shut down
    ```
  
