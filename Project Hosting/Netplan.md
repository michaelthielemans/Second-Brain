## check dhcp info
```
netplan ip leases eno1
```

### change ip address
/etc/netplan/xx-cloud-init.yaml

## Reload netplan configuration
```
sudo netplan apply
```

## Virtual machines and DHCP
When cloning virtual machines the network interface of the new vm will be receiving a new mac address. Normally this would mean that the ip address offered by dhcp will be unique, this is not the case anymore because ubuntu will try to claim an ip not based on mac address.
To solve this issue adjuct the netplan config file.

add the line:
` dhcp-identifier: mac