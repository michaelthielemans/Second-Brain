Dns consists of 3 basic parts

## The stub resolver
- The resolver client service on the host itself
- /etc/hosts file
- `resolvectl status`

## The caching of recursing resolver
Will get the zone information from the master and save it localy for a specific time (=TTL)
When TTL expires : refresh

## The authoritative name server
> The server who holds the primary dns zone.


## Types of records
- A = basic ipv4 record
- AAAA
- CNAME = common name or alias for a record
- PTR = pointer record -> reverse mapping
- NS = name server
- SOA = Start of authority

# Master and slave DNS servers
Primary and secondary DNS servers
- Primary/master = responsible for the content of the dns database
- Secondary/slave = holds a copy of the database
> the copy process of information from the primary to the secondary is called zone transfers
> 