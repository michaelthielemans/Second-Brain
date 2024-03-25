#windows 
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

### Repadmin

```powershell
repadmin /syncall #replicate to all dc's
repadmin /replicate dest-dc01 source-dc01   #pull replication from dst to source
repadmin /showrepl #show the replication status
```
### DCdiag

### Replication monitor

# powershell cmdlets

### Installing new root domain

```powershell
Install-ADDSForest -DomainName "corp.contoso.com"
```

### Installing new child domain

```powershell
Install-ADDSDomain
```

### Install new domain controller in existing domain
```powershell
Install-ADDSDomainController
```