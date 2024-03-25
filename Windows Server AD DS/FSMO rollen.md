#ActiveDirectory 
How to check roles

```powershell
netdom query fsmo
```


RID master via ADUC
PDC via aduc
domain naming master via dom trust
infrastructure master - 1 per domain






schema bekijken via mmc.exe
```powershell
regsv32 schmmgmt.dll
```
vanaf nu is er een extra snapin in mmc beschikbaar

# 5 FSMO roles
Flexible Single Master Operation roles

1. Schema Master = at forest level
2. Domain naming master = at forest level
3. RID master = at domain level
4. PDC emulator / Primary domain controller = at domain level
5. Infrastructure master =  at domain level
## Schema master
Holds a read/write copy of the schema

## Domain naming master
makes sure that a second domain / subdomain with the same name can be created. he makes sure that every domain name is unique.
## RID (Relative ID) master
manages the different pools of RIDs that every DC can manage. Because different DCs are creating and supplying SIDs, their is a possibility for duplicate SIDs . the RID keeps an eye on that by providing each DC with a POOL of RIDs

## Primary DC
- respond to authentication requests
- manage password changes
- manages Group Policy Objects (GPO)
- Users cannot change their passwords without the approval of the PDC Emulator.
- synchronize time in an enterprise
- Password changes done by other DCs in the domain are replicated preferentially to the PDC emulator.
- When authentication failures occur at a given DC because of an incorrect password, the failures are forwarded to the PDC emulator before a bad password failure message is reported to the user.
- Account lockout is processed on the PDC emulator.
- The PDC emulator performs all of the functionality that a Windows NT 4.0 Server-based PDC or earlier PDC performs for Windows NT 4.0-based or earlier clients.

## Infrastructure Master

**Updating references from objects in the local domain to objects in other domains**. There can be only one Infrastructure Master DC in each domain.

