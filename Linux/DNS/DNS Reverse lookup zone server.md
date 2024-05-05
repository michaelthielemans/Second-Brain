
1. Install bind
2. configure own resolv settings
3. add new zone to the name.conf.local configuration
4. Create a new zone file
5. Restart bind service
6. troubleshooting

## 1. Install bind
```bash
dnf update
dnf install bind
```

## 2. config resolver settings

add the root dns server to the file:
>/etc/systemd/resolved.conf  (debian based)
>	-> also check netplan
>/etc/resolved.conf (rhel based)
>	-> managed by 'networkmanager'

sudo service systemd-resolved restart
sudo service systemd-resolved status

resolvectl status
## 3. Add new zone
> vim /etc/bind/named.conf.local

we want the have a reverse lookup zone for the net 10.0.2.0/24
-> the notation will become 2.0.10.in-addr-arpa

```bash
zone "2.0.10.in-addr.arpa" {
		notify no; # new updates will not be notified to slave dns servers
		allow-update {none;}; # no other server is allowed to pull updates
		type master; # this server is the master server
		file "/etc/bind/reverse_zone"; # location of the zonefile
}
```
## 4. Create a new reverse zone file

> Make a copy of the /etc/bind/db.127 zone file and give it a new name
> This file can be used as a template

### Adding records to the new zone file

### Adjust permissions of the new zone file
Root has write all other have only read permissions.
```bash
chmod 644 /etc/bind/ITF_linux
```

## 5. Restart the dns service
```bash
sudo systemctl restart bind9.service
```

## 6. Troubleshooting

check logs in :  /var/log/syslog

If for some reason the dns server is not giving correct answers to the queries -> restart the service and flush all caches

Restart your bind9 service:
```bash
sudo systemctl restart bind9.service
```

Delete the cache of the systemd-resolved-service. How?
```bash
sudo resolvectl flush-caches
```

To verify that flush was successful, use:
```bash
sudo resolvectl statistics
```

Restart the systemd-resolve service:
```bash
sudo service systemd-resolved restart`
```

