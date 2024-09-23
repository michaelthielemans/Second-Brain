Is no declarative language
## Control node = ansible machine
## Managed node => the target machine

## Inventory
Default inventory location: /etc/ansible/hosts
```
[virtualmachines]
10.0.2.4
```

```
ansible all --list-hosts
```
### Playbook
- play 1
	- task 1
		- module 55
- play 2
	- task 55
		- module 55
		- module 44

```
---
- hosts:
. tasks:
	-name:
	ansible.builtin.ping:
	-name:
	ansible.builtin.debug:
		msg: Hallo
```

## Module = unit of conde that ansible runs
## Task = single action or activity