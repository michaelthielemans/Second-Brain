#dns #ActiveDirectory 
On the internet they use mostly a dns with a primary zone and other dns servers host the secondary zone of a domain.

This will not work very well for windows environments, because the dns records of workstations change a lot.
## Netlogon service on domain controllers
Elke domain controller heeft een netlogon service, deze heeft als taak om alle domain controller services ( lees: SRV records) te registreren in de prefered DNS server. Het is mogelijk dat de domain controller ook de preferred dns server is voor zichzelf
### In active directory

DNS zone files are placed into active directory, this way the zone file can be edited on multiple dns (domain controllers) . This is because the domain controllers replicate new changes on the zone between the DCs.
## Why is preferred and alternate dns settings important
a workstation uses the dns server (DC) for queries and registration.

Preferred dns = registrations, queries
alternate dns = used only when preferred dns is down.

#### dns server management console
view the server cache -> view -> advanced

DNS replication mecanism = ip tcp port 53