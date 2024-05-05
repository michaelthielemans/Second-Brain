## Types of access controls:
>• allow transfer
>• allow query
>• allow recursion (recursive queries)

Each of the access control types (allow-transfer, allow-query, ...) can contain:

• address match lists
• access control lists

#### Address match list:
10/8; 172.16 / 12; 192.168 / 16;

#### Access control list:
An ACL is defined with:
acl "name" {address match list; };

### There are 4 predefined ACLs:

**• none** = the empty ACL
**• any** = all possible IP addresses
**• localhost** = all IP addresses of the server on which bind9 runs from the same host system

For example server IP address 192.168.2.3:

=> Then the ACL "Localhost" corresponds with 192.168.2.3 and 127.0.0.1

**• localnets** = all IP addresses and subnets of the server on which bind9 runs

For example server IP address 192.168.2.3 with subnet mask 255.255.255.0

=> Then the ACL “Localnets” corresponds with the IP addresses 192.168.2.0 to 192.168.2.255 and 127.0.0.1


#### Configure acl for a specific zone

edit /etc/bind/named.conf.local

```bash
acl "<name_of_the_acl>"
{<ip_of_the_allowed_host>;};

zone "<name_of_zone" {
		notify yes;
		allow-query {<name_of_the_acl;};
		allow-transfer {<ip_of_slave_server;};
		allow-update {none;};
		type master;
		file "/etc/bind/<zone_file>";
}

```
The <name_of_