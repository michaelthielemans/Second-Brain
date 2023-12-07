# a host looks for a domain controller to authenticate

What does the host knows and what is it looking for so a user can login into his account on that computer.
### The host knows:
> - The DNS server IP address he received from the DHCP server or manual input
> - The DOMAIN NAME (domain.be) he is member of
> - The site name he is in

### He looks for
> - The Ip address of the domain controller he wants to sends an authentication request to.

### Steps to accomplish:
1. The host sends a DNS query to request all the available Domain controllers in the Doman AND Site he belongs to.
2. The DNS server responds with a list of SRV record of all the DCs FQDN.
3. The host chooses a DC from the list based on the [[#Changing priority and / or weight of a domaincontroller]]priority and weight (by default they are all 0 = equal prio and weight).
4. The host sends a query to the DNS to request the ip addresss of the selected DC
5. The DNS server responds with a HOST record with the ip address of the DC
6. The host then starts a communication with the ip address of the DC

If the communication to the first selected DC fails:
1. the host selects the second SRV record he received from the DNS server

### If the client host does not know the site he belongs to
1. The client sends a DNS query to the DNS server, in the request there is the domain name and the service he wants (net logon for example)
2. The DNS server sends a list of SRV records with ALL the DCs in the domain, also DCs from different sites.
3. the host client can then choose from the list a DC. and sends a query to the DNS server to ask for the ip address of the selected DC.
4. The host then can start a communicatin with the DC, if the DC is NOT in the same site as the host, the DC will send the site information the host in fact 


## Location in DNS of the AD services

check the folder in DNS
domain-name -> TCP
-  \_gc
- \_kerberos
- \_kpassword
- \_ldap

#### _msdcs.domain.name
- this is a dns folder specific for microsoft clients and services. It represents the forest root structure.

# DNS scavenge

When scavenging enabled , DNS records that are not updated after a period of time will be deleted.
# Changing priority and / or weight of a domaincontroller
This can be change with a registry key on the domain controller, by default the priority and weight are 0.
The dc with the priority with the lowest value is chosen first!
The _weight_ defines which of the DCs with the same priority, is more favoured than the other. A higher weight means it's favoured more.

1. Navigate to the base key:
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters
2. Under that key, create a DWORD (32-bit) value with the following name:
    Weight: LdapSrvWeight
    Priority: LdapSrvPriority
3. Restart the NETLOGON service to republish the SRV records with the new weights and priorities in DNS:
	`net stop NETLOGON && net start NETLOGON`

Do not alter the priority and weight settings on the DNS service record, because this will be overwritten. this is because dynamic dns updates is enabled.