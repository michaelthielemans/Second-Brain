#windows
# Authorative DNS server
Can return a NO to the query
If the authorative dns has no record for the request he will respond with an 
The dns server of the zone you manage should be authoritative, in fact he is the only dns server who will know all the records inside the zone. (domain)

# Non authorative DNS server
Tries to answer the request but he will start a recursive query for the dns records he does not have. He can not decide if a domain name does not exists of a zone where is he the non authorative of.
# Recursive query

>A client sends a recursive query which means: The query asks the complete answer or a error answer nothin else!

>The DNS server will contact multiple other dns servers in order to respond to the client with a complete answer.

A recursive DNS lookup is where one DNS server communicates with several other DNS servers in order to find the IP address bound to the dns name, and return it to the client. This is in contrast to an iterative DNS query, where the client communicates directly with each DNS server involved in the lookup.

# Iterative query

DNS client allows the DNS server to return the best answer it can give based on its cache or zone data

> The client has to send queries to multiple DNS server in order to find the IP address

1. A clients sends a query to the first DNS server.
2. The DNS server will respond to the query with a referral to another the higher level DNS server that can resolve the next piece in the FQDN. can be answered with a referral to another DNS server
3. If the answer is can be incomplete, so a other dns server should be queried.

# Forwarder

A dns server can be configured to make use of a forwarder. If the name query cannot be resolved using its local zone data or cache, then it will forward the query to the DNS server designated as a forwarder. As a result, root hints method of name resolution will not be used.

The original DNS server that received the initial query will wait briefly for an answer from the forwarder. If that fails, it will attempt to contact the DNS servers specified in its root hints as a last resort.

# Conditional forwarding

Conditional forwarders are DNS servers that only forward queries for specific domain names. Instead of forwarding _all_ the queries it cannot resolve locally to a forwarder, a conditional forwarder is configured to forward a query to specific forwarders based on the domain name contained in the query. Forwarding according to domain names improves conventional forwarding by adding a name-based condition to the forwarding process.

# Root hints

>The root hints are the IP addresses configured inside a DNS server. These are the IPs of the higher level DNS servers.

Root hints is **a list of the DNS servers on the Internet that your DNS servers can use to resolve queries for names that it does not know**. When a DNS server cannot resolve a name query by using its local data, it uses its root hints to send the query to a DNS server.

# DNS caching

Temporarily cache dns records for future fast query resolving.

# DNS zones

A zone is a administrative bubble that can contain a single domain, multiple domains and domains with subdomains. It is an area(bubble) of delegated responsibility to a single manager.

TLD (Top Level Domains zones):  .com.  , .be. ,  .net.
domains: bel.be.  ,   tweakers.net.
subdomains: forum.tweakers.net

it is possible that forum.tweakers.net is in a different zone and blog.tweakers.net is in the same zone as tweakers.net. 

| zones                       | descr                                                                                                        |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| primary                     | read write copy of a dns database                                                                            |
| secondary                   | read only copy of primary                                                                                    |
| stub                        | copy of a zone                                                                                               |
| active directory integrated | a zone file that is replicated across multiple domain controllers with the use of AD replication technology. |
## Start Of Authority (SOA) file
Each zone has a SOA file, this file contains different records: MNAME, RNAME,REFRESH,RETRY,.....
it contains information about that zone: contact info, admin,.....

### Primary zones (= read + write on a zone file)

A DNS server hosting a primary zone is the primary source for information about this zone. It stores the zone data in a local zone file or in AD DS. To create, edit, or delete resource records, you must use the primary zone. Secondary zones are read-only copies of primary zones.

You can store a standard primary zone in a local file, or you can store zone data in AD DS. When you store zone data in AD DS other features are available, such as secure dynamic updates and the ability for each domain controller that hosts the zone to function as a primary and be able to process updates to the zone. When the zone is stored in a file, by default the primary zone file is named `zone_name.dns`, and it's located in the `%windir%\System32\Dns` folder on the server.

When you deploy Active Directory, a DNS zone that is associated with your organisation’s AD DS domain name is automatically created. By default the AD DS DNS zone replicates to any other domain controller configured as a DNS server in the domain. You can also configure Active Directory Integrated DNS zones to replicate to all domain controllers within an AD DS forest, or specific domain controllers enrolled in a particular AD DS domain partition.
### Secondary zone ( = read only copy of a zone file)

A secondary zone is a read-only copy of a primary zone. When the zone that this DNS server hosts is a secondary zone, this DNS server is a secondary source for information about this zone. The zone at this server must be obtained from another remote DNS server computer that also hosts the zone. This DNS server must have network access to the remote DNS server that supplies this server with updated information about the zone. Because a secondary zone is only a copy of a primary zone that is hosted on another server, it can't be stored in AD DS as an Active Directory Integrated zone.

In most cases, a secondary zone periodically copies resource records directly from the primary zone. But in some complex configurations, a secondary zone can copy resource records from another secondary zone.

The dns server that hosts the secondary zone syncs the records from the dns server that holds the primary zone.

### Stub zone

A zone with only links to authoritative dns servers.

For example service.domain5.bel
The stub zone domain5.bel on our dns server has only the information to find the authoritative dns server for domain5. When a request is coming in our DNS server immediately knows where he can find the dns server for domain5. This is faster than when our dns server has to contact the root dns servers first in order to find the dns server domain5.bel

A stub zone only contains information about the authoritative name servers for the zone. The stub zone hosted by the DNS server must obtain its information from another DNS server that hosts the zone. This DNS server must have network access to the remote DNS server to copy the authoritative name server information about the zone.
It is possible that for one stub zone there are links to multiple dns servers that holds that zone ( can be primary or secondary)

You can use stub zones to:

- Keep delegated zone information current. The DNS server updates the stub records for its child zones regularly, the DNS server that hosts both the parent zone and the stub zone maintains a current list of authoritative DNS servers for the child zone.
- Improve name resolution. Stub zones enable a DNS server to perform recursion using the stub zone's list of name servers, without having to query the Internet or an internal root server for the DNS namespace.
- Simplify DNS administration. By using stub zones throughout your DNS infrastructure, you can distribute a list of the authoritative DNS servers for a zone without using secondary zones. However, stub zones don't serve the same purpose as secondary zones, and they aren't an alternative for enhancing redundancy and load sharing.

There are two lists of DNS servers involved in the loading and maintenance of a stub zone:

- The list of name servers from which the DNS server loads and updates a stub zone. A name server may be a primary or secondary DNS server for the zone. In both cases, it has a complete list of the DNS servers for the zone.
- The list of the authoritative DNS servers for a zone. This list is contained in the stub zone using name server (NS) resource records.

When a DNS server loads a stub zone, such as `widgets.tailspintoys.com`, it queries the name servers, which can be in different locations, for the necessary resource records of the authoritative servers for the zone `widgets.tailspintoys.com`. The list of name servers may contain a single server or multiple servers, and it can be changed anytime.

A stub zone is a copy of a zone that contains only those resource records that are necessary to identify the authoritative Domain Name System (DNS) servers for that zone. Typically, you use a stub zone to resolve names between separate DNS namespaces.

When working with sub zones, you should consider:

- The stub zone can't be hosted on a DNS server that is authoritative for the same zone.
- If you integrate the stub zone into AD DS, you can specify if the DNS server hosting the stub zone uses a local list of name servers or the list stored in AD DS. If you want to use a local name servers list, you must have the IP addresses for each name server.

### Reverse lookup zones

In most Domain Name System (DNS) lookups, clients typically perform a forward lookup, which is a search that is based on the DNS name of another computer as it is stored in a host (A) resource record. This type of query expects an IP address as the resource data for the answered response.

DNS also provides a reverse lookup process, in which clients use a known IP address and look up a computer name based on its address. A reverse lookup takes the form of a question, such as "Can you tell me the DNS name of the computer that uses the IP address 192.168.1.20?"

The `in-addr.arpa` domain was defined in the DNS standards and reserved in the Internet DNS namespace to provide a practical and reliable way to perform reverse queries. To create the reverse namespace, subdomains within the `in-addr.arpa` domain are formed, using the reverse ordering of the numbers in the dotted-decimal notation of IP addresses.

The `in-addr.arpa` domain applies to all TCP/IP networks that are based on Internet Protocol version 4 (IPv4) addressing. The New Zone Wizard automatically assumes that you're using this domain when you create a new reverse lookup zone.

The order of IP address octets must be reversed when the `in-addr.arpa` domain tree is built. The IP addresses of the DNS `in-addr.arpa` tree can be delegated to organizations as they're assigned a specific or limited set of IP addresses within the Internet-defined address classes.
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

## PTR - Pointer records

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