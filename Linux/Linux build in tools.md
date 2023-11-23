## SSH -  openSSH

by default SSH uses password authentication
You can also use k

### install openssh server
```
sudo dnf install openssh
```

### connect and login to machine over ssh

```
$ ssh 192.168.1.10 (connect with user account you are logged in locally)
$ ssh michael@192.168.1.10
```

logout = ctrl-d

### ssh config files

user specific ssh config files:
/home/user/.ssh/
### ssh key management

a key is more secure than a password

1. generate key