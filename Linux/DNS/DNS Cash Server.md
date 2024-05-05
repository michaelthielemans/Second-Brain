
1. Install bind
2. Configure own resolv settings
3. Add new zone to the named.conf.local configuration
4. Create a new zone file
5. Restart bind service
6. Troubleshooting

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

## 4. Create a new zone file

> Make a copy of the db.local file and give it a new name
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

