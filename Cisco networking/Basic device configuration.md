#cisco #networking #config

# General config

> `(conf)#hostname <name>`
> `(conf)#ip domain-name <domainname>`
> `(conf)#no ip domainname-lookup`
> `(conf)#no sychro logging`
> `(conf)#username <name> secret <passw>`


> enable passwords:
`(conf)#enable password <this password is not hashed>`
`(conf)#service password-encryption`
`(conf)#enable secret <this password will be hashed>`

>create a key pair for ssh
>```(conf)
>```
```
(conf)#crypto key generate rsa modulus 1024
(conf)#
```

> line config: console + vty virtual terminal
> `(conf)# line console 0`
> `(conf-line)#password .....`
> `(conf-line)#login
> 
>`(conf)# line vty 0 15`  (max 15 concurrent vty sessions)
>`(conf-line)# password ....`
>`(conf-line)#transport input ssh`
>`(conf-line)# login local`
>`(conf)#ip ssh version2`

>management ip address on interface
>`(conf)#interface loopback 0`
>`(conf)#ip address x.x.x.x mask `



# Vlan config

