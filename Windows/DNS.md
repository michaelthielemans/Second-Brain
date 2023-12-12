#windows
# Authoritive DNS server
can return a NO
If the authoritive dns has no record for the request he will respond with an 

# Non authoritive
will always start a recurvice query for the dns records he does not have

# Recursive query

a query that has to be answered
requires a complete answer

# Iterative query

a query from one DNS server to a higher level DNS servver.
can be anwered with a referral to another DNS server

the answer is can be incomplete, so a other dns server should be queried.


# Forwarder

The local dns server sends all his queries to the forwarder.

# Conditional forwarding

requests using a part of the domain name.
this way you can skip 

# Root hints

# DNS caching

Temporarily cache dns records


# DNS zones

|zones | descr|
|--|--|
|primary| read write copy of a dns database|
|secondary | read only |
|stub| copy of a zone |
|active directory integrated | |

# DNS record types

| record | description |
|--|--|
|A| host to ip  |
|PTR | ip to host |
|AAAA | host to IPv6 |
|NS | name server
|SRV | service to IP
|MX | mail service to IP |
|CNAME | alias of a record |

## PTR Pointer records

PTR records are used in reverse DNS lookups; common uses for reverse DNS.

DNS PTR records are stored under the IP address — reversed, and with ".in-addr.arpa" added. For example, the PTR record for the IP address 192.0.2.255 would be stored under "255.2.0.192.in-addr.arpa".

"in-addr.arpa" has to be added because PTR records are stored within the .arpa top-level domain in the DNS. .arpa is a domain used mostly for managing network infrastructure, and it was [the first](https://tools.ietf.org/html/rfc881) top-level domain name defined for the Internet. (The name "arpa" dates back to the earliest days of the Internet: it takes its name from the Advanced Research Projects Agency (ARPA), which created ARPANET, an important precursor to the Internet.)

# Forward and reverse lookup zones

forward lookup = domainname to ip
reverse lookup = ip address to domainname

the dns server will answer to the reverse lookup query with a reversed IP
10.2.3.4 -- will be answered as --> 4.3.2.10



# DNS client
### nslookup command
nslookup -> does not use the local cache, performs immediately a query to the dns server.


# DNS dynamic registration of hosts

A dns registration of a host can be triggered by :
- reboot
- ipconfig /registerdns
- register-dnsclient