Informational:
- /etc/hosts = the file with all static dns names -> for fast dns query.
- /etc/resolv.conf = the file with all the dns servers.

1. use hosts file
2. use resolv.conf

# Systemd-resolved
- is a systemd service
- `systemctl status systemd-resolved
- check the service itself ` resolvectl status`
- config file : ` /etc/systemd/resolved.conf`
	- restart service after editing the config file `systemctl restart systemd-resolved`
- full support of DNSSec and DNS over TLS
# Modes of operation
- recommended mode
- compatibility mode
The mode decides how the /etc/resolv.conf file is used. the resolv.conf file is consulted by other programs who want to send a dns query.
## recommended mode
- systemd-resolver will manage the resolv.conf file
- a symlink is made from /etc/resolv.conf to /run/systemd/resolve/stub-resolv.conf
- it can cause issues with other programs who wants to change the resolv.conf file itselfs

## Compatibility mode
- /etc/resolv.conf is not altered
- in this mode other programs can manage the resolv.conf file