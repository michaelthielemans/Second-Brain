# DNS client commands
```
ipconfig /displaydns
ipconfig /flushdns
ipconfig /all
ipconfig /registerdns
```
```powershell
get-dnsclientcache
clear-dnsclientcache
register-dnsclient
```

# DNS server service commands

```
# how to clear the dns server cache
restart-service dns
clear-dnsservercache

# test dns zone files
Test-dnsserver –ipaddress 10.151.11.111  -zonename “dom.tm”
```