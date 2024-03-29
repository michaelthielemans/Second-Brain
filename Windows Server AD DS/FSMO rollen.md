#ActiveDirectory 
## How to check roles

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
vanaf nu is er een extra snapin in mmc beschikbaar om schema te bekijken. ADSI edit is more ore less also a schema viewer.

# 5 FSMO roles
Flexible Single Master Operation roles

### Forest level master roles
1. Schema Master
2. Domain naming master
### Domain level master roles
3. RID master
4. PDC emulator / Primary domain controller
5. Infrastructure master
## Schema master
Holds a read/write copy of the schema, all the other domain controllers have a read only copy of the schema. This needed because there can only be one version of the schema
## Domain naming master
Makes sure that a second domain / subdomain with the same name cannot be created. He makes sure that every domain name is unique inside the forest. He only has to do a check when creating a new child domain.
## RID (Relative ID) master
Manages the different pools of RIDs that every DC can manage. Because different DCs are creating and supplying SIDs, their is a possibility for duplicate SIDs . the RID keeps an eye on that by providing each DC with a POOL of RIDs.
Every object in active directory has a SID attached to it. 
Every domain has its own domain ID and every SID in the domain starts with the domain ID. The RID master role is therefore not needed at the forest level because every domain has its unique ID.

## Primary DC - PDC
- Respond to authentication requests
- Manage password changes
- Manages Group Policy Objects (GPO), Is the only server which hold the GPO editable version.
- Users cannot change their passwords without the approval of the PDC Emulator.
- Synchronize time in an enterprise
- Password changes done by other DCs in the domain are replicated preferentially to the PDC emulator.
- When authentication failures occur at a given DC because of an incorrect password, the failures are forwarded to the PDC emulator before a bad password failure message is reported to the user.
- Account lockout is processed on the PDC emulator.
- The PDC emulator performs all of the functionality that a Windows NT 4.0 Server-based PDC or earlier PDC performs for Windows NT 4.0-based or earlier clients.

## Infrastructure Master

**Updating references from objects in the local domain to objects in other domains**. There can be only one Infrastructure Master DC in each domain.

