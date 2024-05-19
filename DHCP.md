- Server Service = dhcpd
	- `sudo apt install isc-dhcp-server`
- client service = dhclient

## dhcpd server

`/etc/default/isc-dhcp-server
Specify the interfaces to which the dhcpd service (server) must listen to receive requests
By default, the dhcp server does not listen to any interface

`/etc/dhcp/dhcpd.conf
- Define ranges and options


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