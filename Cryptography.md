#crypto
### Hashing algoritms
- MD5 - legacy
- SHA-1 legacy
- SHA-2 nextgen hashing (SHA256,SHA512,...)
## Symmetric encryption

- DES : data encryption Algoritm
- 3DES : tripple DES , does DES 3 times, trustworthy when used with short key lifetimes
- AES : advanced encryption standard
- SEAL : Software-optimized Encryption Algoritm . this algoritm has a lower impact on CPU resources
- Rivest ciphers (RC) series algorithms : used to secure web traffic like SSL and TLS
## Asymmetric encryption

> Assymmetric keys are used mostly for key exchange, once the 'private' key is exchanged the system will work only with the private key. Unless the key needs to be renewed.
> 
> Unfortunately, asymmetric key systems are extremely slow for any sort of bulk encryption. It is common to encrypt the bulk of the traffic using a symmetric algorithm, such as 3DES or AES and then use the DH algorithm to create keys that will be used by the encryption algorithm.
### Diffie-helman 
- Diffie-Hellman mathematical algoritm, makes it possible to exchange a key between hosts that have never seen before.
- The algoritims works as if you would mix colors and it is impossible to un-mix the colors again.
- It makes it possible to encrypt and send the symmetric key so encryption between to parties can start
- It does not provide authentication. There is no trace that the key is from the intended sender!!!

1. each user chooses a private key = random number.
2. Both parties know the public part. Either be common known variables from the protocol or chosen by one of the users and send to the other.
	1. the known part contains 2 numbers: modulo (n) and base number (g)
	2. both parties will calculate the modulo of the basenumber to the privatenumber
	$$ (g^{private} ) \%  n = public key $$
	4.  both parties will calculate a new key base on their own private key and the receive public key
	$$ (g^{private * public})  \%  n = new private key $$
		Both users will have the same private keys !!!

The main difference between diffie-helman and RSA is that DH will calculate at the and a common private key that is the same on both sides while RSA will use the public key to encrypt and private to decrypt.
DH does not provide authentication

### RSA

- RSA can provide authentication!!
- RSA is used inside PKI , Certificates

#### Steps:
1. Both client will create a public / private key pair
2. one client encrypts its message with his private key
3. this message can only be opened by the public key of that sending client. -> this will guarantee authentication
4. The client that just has received the message can respond to that message by encrypting the response with the **receivers public key** , this way the sender is confident that the message can only be decrypted by the receiving client because he has the corresponding private key to decrypt the message. -> this way the symmetric key is transferred between the two clients.

#### Certificates and PKI (*Public Key Infrastructure*)

> Everybody has the public keys of the trusted known certificate authorities. These public keys can be used to check if someone is trusted by the Certificate authority or not.

The reason for a certificate to be signed by a CA is:
> I guarantee that  ==_this_public key_==  is really owned by the guy with ==_that_== name

Certificate Signing request
1. A server wants to request a certicate.
2. The server/webserver creates a CSR (certificate Signing Request). It is in fact his own public part of his keypair + other variables like the common name,......
3. This CSR is send to a Certificate Authority.
4. The CA checks if all the metadata and information is valid and correct. If so it will generate a certificate with all the information.
5. The certificate is signed with the PRIVATE key of the Certificate authority.


