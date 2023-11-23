#crypto #security
# cryptography
### Hashing algoritms
- MD5 - legacy
- SHA-1 legacy
- SHA-2 nextgen hashing (SHA256,SHA512,...)

## Symmetric encryption

- DES : data encryption Algoritm
- 3DES : tripple DES , does DES 3 times, trustworthy when used with short key lifetimes
- AES : advanced encryption standard
 -SEAL : Software-optimized Encryption Algoritm . this algoritm has a lower impact on CPU resources
- Rivest ciphers (RC) series algorithms : used to secure web traffic like SSL and TLS
## Asymmetric encryption

- Diffie-Hellman mathematical algoritm, makes it possible to exchange a key between hosts that have never seen before
- Unfortunately, asymmetric key systems are extremely slow for any sort of bulk encryption. It is common to encrypt the bulk of the traffic using a symmetric algorithm, such as 3DES or AES and then use the DH algorithm to create keys that will be used by the encryption algorithm.