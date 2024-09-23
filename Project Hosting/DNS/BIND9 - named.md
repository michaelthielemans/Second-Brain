Most used DNS server = BIND9
```
systemctl status bind9.service
```

Informational:
- /etc/hosts = the file with all static dns names -> for fast dns query.
- /etc/resolv.conf = the file with all the dns servers.

1. use hosts file
2. use resolv.conf

## Installation of DNS server
### Package installation
```
sudo apt install bind9
sudo apt install dns-utils

# check if successfully installed
named -v
```
### Config files
```
# contains information about the zone and the location of the zonefile
/etc/bind/named.conf.local

# system information
/etc/bind/named.conf.options
/etc/bind/named.conf.default-zones
```
Data from zone-transfers are stored in:
`/var/cache/bind`
#### /etc/bind/named.conf.local
```sh
zone "name_of_zone" {
		notify no; # no slave nameservers for this zone
		allow-update {none;}; # dynamic dns is not allowed
		type master;
		file "/etc/bind/zonefile_name";	
};
```

#### Zone file (forward lookup zone)

```conf
;
; BIND data file for local loopback interface
;
$TTL     604800
@        IN      SOA    onzepc.domain. michael.mail.
						2        ; Serial
						604800   ; Refresh
						86400    ; Retry
						2419200  ; Expire
						604800 ) ; Negative Cache TTL
;
@          IN     NS   subdomain.domain.
;
Server0    IN     A    192.168.1.5   
server1    IN     A    192.168.1.6  
```
> michael.mail = michael@mail. the @ cannot be used because @ has another meaning in the file.

| parameter          | description                                                             |
| ------------------ | ----------------------------------------------------------------------- |
| $TTL               | value in seconds                                                        |
| serial             | version # of the zone file                                              |
| refresh            | time interval between checks if there is a new serial                   |
| retry              | time interval between attempts when master is unavailable               |
| expire             | time interval for requesting a zone-transfer (even serials is the same) |
| negative cache TTL | how long is this zone is kept in cache                                  |

## Logs
```
sudo tail -f /var/log/syslog
```