FTP: file transfer protocol
FTPS: File Transfer protocol over SSL
FTPeS: File Transfer protocol explicit over SSL
SFTP: SSH based FTP
# FTP

FTP connection build-up
port 21 control connection
port 20 data connection
### FTP modes
#### Active FTP

Active FTP was introduced in the early days of computing
Here's a simplified explanation on how an active mode connection is carried out, summarized in two steps. Some relevant steps (e.g. ACK replies) have been omitted to simplify things.

1. A user connects from a random port on a file transfer client to FTP port 21 on the server. It sends the PORT command, specifying what client-side port the server should connect to. This port will be used later on for the data channel and is different from the port used in this step for the command channel.

2. The server connects from port 20 to the client port designated for the data channel. Once the data connection is established, file transfers are then made through these client and server ports.

#### Passive FTP
> Why using Passive mode:
> The most important difference is that with passive ftp the session for transfering the data is initiated by the client and not the server, this makes it possible that the client can be behind a firewall or nat-router. (He is the outgoing session initiator)

In passive mode, the client still initiates a command channel (control connection) to the server. However, instead of sending the PORT command, it sends the PASV command, which is basically a request for a server port to connect to for data transmission. When the FTP server replies, it indicates what data port number it has opened for the ensuing data transfer.

Here's how passive mode works in a nutshell:

1. The client connects from a random port to port 21 on the server and issues the PASV command. The server replies, indicating which (random) port it has opened for data transfer.  

2. The client connects from another random port to the random port specified in the server's response. Once connection is established, data transfers are made through these client and server ports.

## FTP session buildup

An FTP connection consists of four steps:

- User authorization
- Setting the control connection
	- Server and client exchange commands for initiating data transfer over the control connection
- Setting the data connection
- Terminating the connections

FTP makes use of the underlying TCP protocol

## Authorization
Access to an FTP server can be obtained in 2 different ways:
- Anonymous
- Authorized
#### Anonymous mode
In anonymous mode, clients can access the FTP server with a standard user called 'anonymous' or 'ftp’.

A password is not required, but it is a good idea to use your email address as a password for this ftp connection over the Internet.

An anonymous user can access the homedirectory of the ftp user account, namely /srv/ftp; unless otherwise included in the configuration.

#### Authorized mode

the user must have an Ubuntu username and password.
An authorized user starts in the homedirectory of this user, namely  /home/username.
Access to other folders depends on the user's permissions


## Transfer modes

1. Stream mode: Data is sent as a continuous stream, relieving FTP from doing any processing. Rather, all processing is left up to TCP
2. Block mode : FTP breaks the data into several blocks (block header = descriptor code + byte count (=# bytes in the data field) and the data field) and then passes it on to TCP.
3. Compressed mode: Data is compressed using a simple algorithm (usually [run-length encoding](https://en.wikipedia.org/wiki/Run-length_encoding)). Run-length encoding, RLE, is the replacement of repetitive patterns in data by the number of repetitions plus what had to be repeated.


## VSFTPD
- vsftpd stands for "very secure FTP daemon"
- Security: one of the most important points for the developer Chris Evans
- vsftpd can be run in chroot mode
- which means that a program (in this case vsftpd) is put in its own root folder, and that it can no longer access files/programs outside that folder - the program is supposedly "locked".
- should the FTP server be hacked, the potential attacker would be locked in a box that is not connected to the rest of the system and therefore could do relatively little damage

# FTPS
- FTPS is FTP over SSL.  
- FTPS supports security methods such as passwords, client certificates, and server certificates.  
- FTPS great alternative to FTP.  
- Uses TLS and SSL to encrypt server connections.
- FTPS can make a meaningful difference to your file transfer security, let’s dive into the main choice you’ll have when using FTPS: whether to use explicit or implicit FTPS.

## Explicit FTPS
- allows clients to request the server to create a secured session using SSL/TLS (as mentioned above).
- This session is created on port 21 which, until a secure connection is requested, is insecure.

## Implicit FTPS
- Allows clients to connect to an implicit port (Port 990) which already has secure connections baked in without requesting for there to be one.
- Implicit FTPS makes use of a dedicated port in order to allow for port 21 to be left open.
- Implicit FTPS is considered much stricter when it comes to establishing a connection that is secure.
- If the recipient fails to comply with the security request, the server immediately drops the connection.
- Implicit FTPS is more strict than explicit FTPS when it comes to establishing a secure connection. In fact, the entire FTP session is encrypted, in contrast to flexibility you have when using explicit FTPS. However, implicit FTPS is considered a deprecated protocol, meaning that it not the current standard.  
- Uses port 989 for the data channel and port 990 for the control channel.


# SFTP
- SSH File Transfer Protocol (or Secure File Transfer Protocol), is a secure file transfer protocol used to secure and send file transfers over secure shell (SSH).
- SFTP, as a network protocol, implements algorithms to encrypt files as they transfer between systems.
- SSH uses Advanced Encryption Standard (AES) to encrypt data.
- AES is a symmetric block cipher that leverages complex mathematics and the unique properties of prime numbers to encrypt data with a key, the length of which determines the difficulty of breaking the cipher. Typically, this means the use of AES-128 or AES-256 algorithms, which use a 128-bit or 256-bit key respectively.
- SSH uses a hashing algorithm, usually SHA-2, to determine data integrity. A “hash” is a unique alphanumeric value created by processing the data through a hashing algorithm.
- The idea is that if the data is run through the same hashing algorithm, it will produce an identical hash. Accordingly, if data produces a different hash than the one provided, it signals that the data has been modified.
- When the file transfer protocol starts, it first sends a SSH_FXP_INIT  (including its version number) packet to the server. The server responds with a SSH_FXP_VERSION packet, supplying the lowest of its own and the client's version number. 

Both parties should from then on adhere to version of the protocol.