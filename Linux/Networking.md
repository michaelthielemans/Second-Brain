#linux
## DNS resolving config
/etc/nsswitch.conf -> define the order of how dns queries should be resolved (DNS or local hosts file)
/etc/resolver.conf -> list with all the ip of dns servers
/etc/hosts -> manual ip - to - dns name

### restarting DNS client service
```
sudo /etc/init.d/bind9 restart
```
### DNS
```
dig <dnsName>
host <ipaddress
host <nameofmachine>
host -t
```
## IP interfaces
```
ifconfig #becoming deprecated
ip a
ip route
route  #becoming deprecated
ping
netstat  #becoming deprecated
ss -s  #show socker -statistics
```

### Ports
File with all the wel known ports
- /etc/services