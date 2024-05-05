# DNS stub resolver 
- The client itself who is querying the dns requests.
-  The stub resolver has its own cache
- The configuration is defined in the file /etc/systemd/resolve.conf

Delete the cache of the systemd-resolved-service. How?
`sudo resolvectl flush-caches`

To verify that flush was sucessfull, use:
`sudo resolvectl statistics`

Restart the systemd-resolve service:
`sudo service systemd-resolved restart`

## Dns resolving steps from a client

1. check the local file /etc/hosts
2. run the resolve service

Forward mapping = Name -> ip address
reverse mapping = ip address -> name

## Types of DNS servers
- Primary
- Secondary
- Caching

> - primary name server is in charge of records in the zone file 
> - secondary name server has a read-only copy of the zone file.
	The zone file is updated periodically with zone-transfers
	zone transfer settings are defined in the SOA

Caching name server:
>• Will get the zone information from the master and save it locally for a specific time (= TTL value)
>• Will reply with this local info as long as the TTL value is not expired
>• TTL expired: refresh


negative time to live -> wanneer er een foute opzoeking is, wordt bepaald in SOA


# BIND = “Berkely Internet Name Deamon”
### Versions of bind
BIND4 (old version)
BIND9 (latest version)

### Install bind
sudo apt-get install bind9
sudo systemctl restart bind9.service

### Configuration file locations
#### Location of the configuration files
>/etc/bind/named.conf

>/etc/bind/named.conf.local
>	Here you define the available zones and its settings + the location of the linked zone file.
>
```bash
zone 'zonename' {
		notify no; #there are no slave name servers for this zone
		allow update {none;}; # determine if dynamic dns is used
		type master;
		file /etc/bind/zonename
}
```

>/etc/bind/named.conf.options
>/etc/bind/named.conf.default-zones
#### Location of the zone files itself with all the records in it.
> /etc/bind/db.local = the example file

#### For reverse lookup zones

make a copy of the db.127 file = the example file for reverse lookups.
### Create new zone file
Copy the db.local file to <zonename>

### Cache location
> /var/cache/bind

### Check version of installed DINB
> named –v


stub resolver

2 serial -> vversie
refresh -> when there is a need to update

neg cache -> if a query is reci


@ -> corresponds with the current zone