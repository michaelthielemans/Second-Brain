### Add a new keypair to ssh
`sh-keygen -t ed25519 -C "michaelthielemans@gmail.com"

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


## Check which ssh keys are available on your machine
`ls -al ~/.ssh
this list the directory with all the private - public keypairs