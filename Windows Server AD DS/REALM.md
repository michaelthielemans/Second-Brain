active directory

LDAP
Kerberos


## realm is used for building a trust between unix and AD


realm trust



indien DC met alle FSMO rollen crashed -> neem andere DC en neem de FSMO rollen over.

dit is in princiepe geen probleem alleen bij de RID kan het zijn dat de nieuwe dc niet over dezelfde info beschikt als de vorige DC.


### Transfer fsmo roles
= het netjes oversdchakelen van rollen


### Seize fsmo roles

= wanneer de dc kapot is die de rollen had en je moet deze overzetten naar een andere DC.


# AD disaster plan

- when a DC crashes
	- restore the DC from backups
# AD upgrade plan

- (optional) move the FSMO roles
- demote the DC
- install new machine
- promote the DC + get FSMO roles back.
