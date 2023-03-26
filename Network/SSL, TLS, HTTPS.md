# SSL, TLS, HTTPS

## What is so important about HTTPS
Without https, the communication between the browser and the server is in plain text. This means that the password you enter or the credit card number you send over the internet can be read by anyone who has the ability to intercept it. 

HTTPS is designed to solve this problem. To make the data sent over the internet unreadable by anyone other than the sender and receiver. Https is an extension of the HTTP protocol. With HTTPS, data is sending an encrypted form using something called TLS. TLS stands for Transport layer security. If the encrypted data gets intercepted by a hacker. All they see is jumbo data. 

## TLS handshake
There are several steps:

1. just like in the case for HTTP, the browser establishes a TCP connection with the server.
2. This is where the TLS handshake begins. The browser sends a client hello to the server. In this hello message, the browser tells the server the following things:
   1. What TLS version it can support. It could be TLS 1.2, TLS 1.3, etc.
   2. What cyber suit he supports. A cyber suit is a set of encryption algorithms to use to encrypt data.
    
   <br/>
   After receiving the client hello, the server gets to choose the cyber suit and the TLS version to use based on the options it got from the client. It sends those in the server hello message back to the client. 
   The server then sends the certificate to the client. The certificate includes a lot of different things. One of the key things is the public key for the server. The client uses the public key in something called asymmetric encryption. In asymmetric encryption, a piece of data that is encrypted by a public key can only be decrypted by teh private key.
   
   <br/>
3. This is the step where the client and the server come up with a share encryption key to use to encrypt data. This is how client sends an encryption key safely to the server over the wide open internet. All this is done in the client key exchange message. The exact detail varies depending on the Cyber Suite used. here we use RSA as an example since it is the easiest to understand: with RSA, the client generates an encryption key also called a session key. Encrypts it with the server public key and send encrypted session key to the server over the internet. The server receives the encrypted session key and decrypts it with its private key. Now both sides hold the session key.
4. We use the session key and agree upon cyber suite to send encrypted data back and forth.

### Why asymmetric encryption?
The main reason is that symmetric encryption is computationally expensive. It's not really suitable for bulk data transmission.

## Note
The handshake we talked about applied to TLS 1.2 while the latest version is TLS 1.3. And TLS 1.3 is supported on all major browsers. As we can see in our illustration, TRS 1.2 takes two network round trips to complete. This is one of the major improvements of TLS 1.3. It optimizes the handshake to reduce the number of network round trips to one.

The second final point is in the explanation above is we use RSA for asymmetric encryption to securely exchange the symmetric session key. Again, we choose RSA because it is easy to understand. However, asymmetric encryption is not the only way to share the session key between the client and the server. In fast, in TLS 1.3, RSA is no longer supported as a method for key exchange. Diffie-hellman is a more common way nowaways for exchanging session keys. Diffie-hellman is complicated but in a nutshell, it uses some advanced math involving large prime numbers to derive a share session key without ever transmitting a public key over the network.