#windows 

Different types of encryption are :
- IIS HTTPS
- IPSEC
- L2TP

## SSL and TLS encryption
- SSL = secure sockets layer (deprecated)
- TLS = Transport Layer security

>**Transport Layer Security (TLS) is the upgraded version of SSL that fixes existing SSL vulnerabilities**. TLS authenticates more efficiently and continues to support encrypted communication channels.
  Now TLS is used as a underlaying encryption technology for HTTPS, in the past https used SSL


- TLS provide authentication and encryption
- TLS uses certificates to establish key exchange in order to be able to have a encrypted communication session
- TLS is a protocol stack and it is using multiple layers on the OSI model.

With TLS and SSL the source and destination ports are not encrypted.

# IPSEC

- IPSEC encrypts the layer 3 payload.
- IPSEC in conjunction with NAT can be a problem because the layer for information is encrypted, this means that NAT cannot read the port information. Also NAT will alter the dest and source port of packets, since this values are protected with a integrity hash in the AH layer NAT will not work.

## IPSEC packet structure

In a IPSEC packet a AH field is added between the IP header and the payload.
This AH (Authentication header) function is to:
	- make sure the payload and the IP header data is not altered (replay attack). By calculating a hash sum of the information and placing the result in the AH header.

## 2 modes of operation: TRANSPORT and TUNNEL mode

#### Transport mode
Is the easiest mode
>Is used to protect an end-to-end conversation between two hosts. This protection is either authentication and/or encryption, but it is not a tunneling protocol. It has nothing to do with a traditional VPN: it's simply a secured IP connection

## Configure IPSEC on windows

mmc.exe -> add snap-in : IP security policy management
1. create ip security policy
2. name for example -> for example: very secure ping
3. no activate default rules ( if the default rules are selected -> this will use kerberos)
4. add rule
	1. does not specify tunnel
	2. lan
	3. ip filter list -> add (= filtering WHEN the policy is applied)
		1. new filter name
		2. my ip address =  choose source ip address
		3. a specific address -> ip of counterpart
		4. select ICMP
	4. filter action
		1. new name
		2. negotiate security
		3. do not allow
		4. integrity (is it spoofed) + encrypt. , 
	5. auth method
		1. select the tools to do the 
		2. use preshared key - the same key need to be used on both ends.
		3. kerberos = username + passw like AD, voor kerberos ath you always need a good connection to the domain controllers TGS