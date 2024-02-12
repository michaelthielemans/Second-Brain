#linux 
configuration management
## ssh config

Manually connect the first time over ssh to the server , so the ssh key fingerprint can be saved.

# Inventory

### Default location
/etc/ansible/hosts

# Modules
Modules can be downloaded from ansible galaxy

Modules are the pieces in the playbook that do the actual work!

# Ad-hoc commands
```
ansible <name_of_host> -m <name_of_module> -a <parameters>

ansible 192.168.1.10 -m find -a "paths=/tmp file_type=file"
```