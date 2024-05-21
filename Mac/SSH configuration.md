#ssh #security 
### Add a new keypair to ssh
`ssh-keygen -t ed25519 -C "michaelthielemans@gmail.com"

### You need to specify a filename.
 The file will be saved in the ~/.ssh/ directory

> Also open the ~/.ssh/config file and add the allowed host to it
 For example:
```text
  Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

>[!info] if you do not enter a passphrase after the key generation process , omit the `useKeyChain yes` line.


### Add the key to the ssh agent: (not always needed)
If you have a passphrase on the private key you can add it to the mac keychain by adding the ` --apple-use-keychain` parameter.
```shell
ssh-add --apple-use-keychain ~/.ssh/<file_privatekey>
```

## Check which ssh keys are available on your machine
`ls -al ~/.ssh
this list the directory with all the private - public keypairs