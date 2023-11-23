#cisco #security #acl
- An ACL is a series of IOS commands that are used to filter packets based on information found in the ==packet header==
- An ACL uses a sequential list of permit or deny statements, known as access control entries (ACEs).
- ACEs are also commonly called ACL statements
## What can ACL accomplish
>Limit network traffic to increase network performance
>Provide traffic flow control
>Provide a basic level of security for network access
>Filter traffic based on traffic type
>Screen hosts to permit or deny access to network services
>Provide priority to certain classes of network traffic

>[!info] ACLs do not act on packets that originate from the router itself.
## ACL Types

1. Standard ACLs permit or deny packets at ==layer 3== and based only on the ==source IPv4 address==
2. Extended ACLs - ACLs filter at ==Layer 3== using the ==source and / or destination== IPv4 address. They can also filter at ==Layer 4== using ==TCP, UDP ==ports, and optional protocol type information for finer control.

### Named or Numbered ACLs ?

>[!info] ACLs can have a number or a chosen name. It is preferred to give ACLs a name
- ACLs numbered 1-99, or 1300-1999 = standard ACLs,
- ACLs numbered 100-199, or 2000-2699 = extended ACLs.

### Named ACLS

>An inbound ACL filters packets before they are routed to the outbound interface. An inbound ACL is efficient because it saves the overhead of routing lookups if the packet is discarded.
>An outbound ACL filters packets after being routed, regardless of the inbound interface.


## Operating steps

1. The router extracts the source IPv4 address from the packet header.
2. The router starts at the top of the ACL and compares the ==source IPv4 address== to each ACE in a sequential order.
3. When a match is made, the router carries out the instruction, either permitting or denying the packet, and the remaining ACEs in the ACL, if any, are not analyzed.
4. If the source IPv4 address does not match any ACEs in the ACL, the packet is discarded because there is an ==implicit deny ACE== that is automatically applied to all ACLs.

>[!error] The last ACE statement of an ACL is always an implicit deny that blocks all traffic. It is hidden and not displayed in the configuration.

>[!info] An ACL must have at least one permit statement otherwise all traffic will be denied due to the implicit deny ACE statement.


## Wildcard Masks in ACLs

0.0.0.0 -> match everything
0.0.0.255 -> match only the first 3 octets

example:
match a host ip
```
R1(conf)#access-list 10 permit 192.168.1.1 0.0.0.0
```

Match a network/subnet
```
R1(conf)#access-list 10 permit 192.168.1.0 0.0.0.255
```

Match the subnets 192.168.==16-31===.0/24 (last 4bit of the third octet )
```
R1(conf)#access-list 10 permit 192.168.16.0 0.0.15.255
```

##### Wildcard mask Calculations method

$ACE wildcard = \frac{255.255.255.255}{- subnetmask} = \frac{255.255.255.255}{- 255.255.255.0} = 0.0.0.255$

#### Wildcard Mask Keywords
- host = This keyword substitutes for the 0.0.0.0 mask
- any = This keyword substitutes for the 255.255.255.255 mask

## Max limit ACLs on interface = 4
- One outbound IPv4 ACL.
- One inbound IPv4 ACL.
- One inbound IPv6 ACL.
- One outbound IPv6 ACL

# config commands

```
Router1#show access-lists
Router1#show run | access-list
Router1#clear access-list counters <acl name or number>
```

>With the show access-lists command you get an overview of all the configured access-lists and their ACE (Access control entries).
>Each ACE within a ACL has its own sequence number. You can use this sequence number to modify a specific ACE.
### Command reference

|command| description  |
|---|---|
|`access-list-number`|Number range is 1 to 99 or 1300 to 1999|
|`deny`|Denies access if the condition is matched|
|`permit`|Permits access if the condition is matched|
|`remark text`|(Optional) text entry for documentation purposes|
|`source`|Identifies the source network or host address to filter|
|`source-wildcard`|(Optional) 32-bit wildcard mask that is applied to the source|
|`log`|(Optional) Generates and sends an informational message when the ACE is matched|
### Create numbered standard ACL

```
Router1(config)#access-list <accesslistnumber> {deny|permit|remark} source <sourcewildcard>
```

### Create named standard ACL

```
Router1(config)#ip access-list standard <name>
Router1(conf-std-nacl)#remark <add custom remark>
Router1(conf-std-nacl)#permit host <hostip>
Router1(conf-std-nacl)#deny host <hostip>
```

>[!info] ACL names are alphanumeric, case sensitive, and must be unique

### Create numbered extended ACL

```
Router1(config)#access-list 10 permit tcp any any eq www
is the same as
Router1(config)#access-list 10 permit tcp any any eq 80

get a list of the available port protocol names
Router1(config)#access-list 10 permit tcp any any eq ?

Allow only returning web traffic
Router1(config)#access-list 10 permit tcp any any eq 80 established
```

### Create named extended ACL

```
Router1(config)#ip access-list extended <name>
Router1(conf-std-nacl)#remark <add custom remark>
Router1(conf-std-nacl)#permit tcp <subnet> <wildcard> eq 80
Router1(conf-std-nacl)#permit tcp any <subnet> <wildcard> established
```
### Remove an ACL
```
Router1(conf)#no access-list <ACL_name/number>
```

### Remove an ACE from an ACL

First check the sequence number of the ACE
```
Router1#show access-lists
```
Now you now the sequence number, first go inside the ACL , then point to the ACE
```
Router1(conf)#access-list SURFING
Router1(conf-ext-nacl)#no <sequence_number>
```
### Link/bind an ACL to an interface

```
Router1(conf-if)#ip access-group <ACL number|ACL name> {in | out}
```


