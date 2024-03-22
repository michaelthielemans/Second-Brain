#ActiveDirectory 

# The AD Database
>Each domain controller has a Active Directory database NTDS.DIT , inside this database are the following partitions.

Forest wide replication
- Schema partition
- Configuration partition
- Global catalog partition
- application partition

Domain wide replication
- domain partition
### With the active directory forest structure you can manage your domains to solve:
- organisational needs
- to solve problems with replication.
	- if you have a remote site you can give that site a separate subdomain , this way you dont need to replicate 

## The domain partition
- It contains all the information you can find in ADUC
- This partition is replicated across all DCs inside a DOMAIN
## The configuration partition
- Contains all the information you can find in Sites and services
- This partition is replicated across all domain controllers in the forest also MSexchange properties
## The schema partition
- Contains all the templates of the AD objects
- Replicated across the complete forest.
- can be edited with AD schema console

For example inside the schema is a template of how a user account looks like, which properties and attributes it has, and so on....

A domain installation of exchange will extend the schema.

## The application partition
- An application can make use of this partition so it benefits from the replication mechanism.
- For example it contains The DNS zone files
- Is replicated across the full forest.

When you make your dns active directory aware, AD will take care of the replication of the zone files across the dns server (domain controllers)

## The global catalog partition
- only available on Domain controllers that have the 'Global Catalog' Function
- This partition is replicated to every Global Catalog inside the forest.
- In deze partition wordt een mini- versie van de domain partition bewaard. De Global Catalog partition bevat niet alle attributen van objecten die in de domain partition staan.

De global catalog partition zal van alle users, computers, en andere object in de domain partition die gegevens opnemen die :

- Uniek zijn, (bvb. Een username is een unieke naam, en is handig voor search doeleinden)

- Statisch zijn (bvb. De geboordtedatum van een user nemen we in de GC partition op omdat het een goed criterium is voor een search, en omdat het nooit kan veranderen)

- En nuttig zijn voor een search opdracht (een paswoord is dan wel uniek, maar verandert constant, en het heeft geen zin om dit bij te houden, want we doen nooit een zoekopdracht naar een user die een bepaald paswoord heeft)

- Op deze manier beschikken we over een gereduceerde versie van de domain partition waarin we snel naar nuttige informative kunnen zoeken. Andere domains en domain controllers kunnen op die manier informatie op een snelle manier in het forest terug vinden.