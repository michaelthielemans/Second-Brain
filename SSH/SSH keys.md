## Creating keypairs

```
ssh-keygen -t ed255
```
## ssh client <-> server connection

The ssh client uses the private key from the keypair
The ssh server needs the public key from the keypair

## location of the private keys
By default the private keys are stored in ~/.ssh/


## Making use of multiple private keys

When you want to store multiple private keys in the .ssh directory you can use the .ssh/config file to define which private key needs to be used when

For example:
```
# GitLab configuration
Host gitlab.com
    HostName gitlab.com
    User git
    IdentityFile ~/.ssh/private_key_gitlab

# GitHub configuration
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/private_key_github

```

