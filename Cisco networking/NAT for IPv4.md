#cisco
Network address translation

# Static NAT
>- Is a 1 to 1 translation
>- One private to one public IP

# Dynamic NAT (also known as pooled NAT)
> - uses a pool of inside global addresses
> - first come first served based

>[!info] Can be combined with PAT

# NAT addresses

> Inside addresses are administered by us

> Outside addresses are public

> Inside global = ip used to go outside


```mermaid
|a|->|b|
```


# PAT - port address translation

if the same port is used by the inside local address with a request = port number + 1

### ICMP requests

query-id instead of port number


# NAT64

will redo the encapsulation of the ip header.

# NAT configuration

## Configure Static NAT
```
R2(config)#ip nat inside source static 192.168.10.254 209.165.201.5
```