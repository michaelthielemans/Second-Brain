# Methods of allocation
## Manual allocation (mac-address)
- manually assign a IP to a mac address
- IP always stays the same also after renewal

## Dynamic allocation (lease-time)
- pool of addresses
- IP is offered for a specific period, after the periode the client has to renegotiate in order to be able to use the address even further
- If ip is not used anymore the ip is available for another client
## Automatic allocation (permanently)
- pool of addresses
- lease period is permanently
- client does not need to renew its lease


# DHCP daemon/Service
- Server Service = dhcpd
	- `sudo apt install isc-dhcp-server`
- client service = dhclient
## Install dhcp server
```
sudo apt install isc-dhcp-server
```

## dhcpd server configuration

#### Config files

> `/etc/default/isc-dhcp-server
>
>Specify the interfaces to which the dhcpd service (server) must listen to receive requests
>By default, the dhcp server does not listen to any interface


>Define ranges and options
>`/etc/dhcp/dhcpd.conf



Restart service after changing configs
```
sudo systemctl restart isc-dhcp-server.service
```

### check if dhcp server is listening
`netstat -uap`
### Check dhcp client status and logging
`sudo dhclient -v enp0s3


`cat /var/log/syslog | grep -Ei ‘dhcp’ `

```
journalctl -n 20 # last 20 logging lines
journalctl -t dhcp
journalctl -u isc-dhcp-server
```