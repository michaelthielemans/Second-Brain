
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

```bash
zone "ITFlinux" {
		type slave;
		file "name_of_zone_file";
		masters { <ip_of_dnsmasterservers};
};
```

The added rules indicate a number of things:

- the server is a slave server for the "ITFlinux" zone
- the server maintains a file for this zone under the /var/cache/bind directory, named “auto_ITFlinux”.

**The /var/cache/bind directory** is the default directory for zone files,
apparmor grants the deamon "named" write permissions to this directory.
This file is provided to the slave server through a zone transfer (data transfer) from the master name server to the slave name server.
- The master server can be reached at the IP address 10.0.2.10.


## Adding logging

```bash
logging {
	channel default_debug;
	file "/var/log/named.run";
	severity dynamic;
};
```
- BIND9 will send debug messages related to DNS to a separate file.
- After all, all kinds of debug messages end up in syslog (in the long run: becomes a very large and unclear file).
- The named daemon is executed as the user "bind".
- The logfile has to be created, because this will not happen automatically.
- Therefore we must change the owner of this file to the user "bind".

`sudo touch /var/log/named.run
`sudo chown bind /var/log/named.run

- Before the named daemon can write data to the log file, the AppArmor profile must be updated.

How?

- First we need to adjust /etc/apparmor.d/usr.sbin.named by adding the following line:

`/var/log/named.run w,

(! pay attention to the comma; place this line with the other named lines!)
After this we need to reload the apparmor profile:

`sudo cat /etc/apparmor.d/usr.sbin.named | sudo apparmor_parser -r
## 4. Adjust the named.conf.local on the master dns server

notify yes;
allow-transfer {<ip_of_the_slave_server>;};

### 5. Add record pointing to the slave server on the master server

In the corresponding zone file on the master server, make sure that ALL slave servers have a name record as well as an address record in this zone file !!

Updating the zone file on the slave server will not work if we don’t increase the serial number of the zone file on the master.

### Adjust permissions of the new zone file
Root has write all other have only read permissions.
```bash
chmod 644 /etc/bind/ITF_linux
```

## 6. Restart the dns services
```bash
sudo systemctl restart bind9.service
sudo service systemd-resolved restart
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

