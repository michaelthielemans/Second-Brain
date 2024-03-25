#ActiveDirectory #windows  

# The AD Database
>Each domain controller has a Active Directory database NTDS.DIT , inside this database are the following partitions.

## NTDS.dit
Is the database file for AD
It contains the following partitions:
1. Domain partition = ADUC content
2. Schema partition = templates of all the objects => attribute definitions
3. Configuration partition = sites and domains, replication settings
4. Application partition  = DNS, ...
5. Global catalog partition (if DC is Global catalog server)

### Forest wide replication
- Schema partition
- Configuration partition
- Global catalog partition
- Application partition (it depends on the settings)

### Domain wide replication
- domain partition
- application partition (it depends on the settings)
## With the active directory forest structure you can manage your domains to solve:
- Organisational needs
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
Schema aanpassingen kunnen niet zomaar ongedaan maken! let dus op
## The application partition
- An application can make use of this partition so it benefits from the replication mechanism.
- For example it contains The DNS zone files

When you make your dns active directory aware, AD will take care of the replication of the zone files across the dns server (domain controllers)

> There can be multiple application partitions inside the AD database!!!
> Each of these application partition is named with a unique identifier. You can check it inside adsi edit tool.
> For example there can be 2 application partitions for dns data. One is used to be replicated across the whole forest (named ForstDNSZones) while the other is only replicated inside the domain (named DomainDNSZones).

The DNS can be opened by adsi edit or with de DNS configuration tool. In the DNS management tool you can specify to which domains/domain controllers the DNS configuration is replicated to. That way the DNS application partition can become a partition that is replicated across the specified domain controllers.

#### DNS inside the application partition
Show all the current  DNS application partitions that are in the forest with cmdline
```cmd
DNSCmd <nameofDC> /EnumDirectoryPartitions
```

Create additional application paritions
```cmd
DNSCmd <nameofDC> /CreatedirectoryPartiton <nameofthepartition.domainname.local>
#This command will create a new partition, therefor it also changes the config in the configuration partition.

repadmin /syncall <DCrunfrom> /APeD
#flags are case-sensitive
# /APeD 'All-Push-eForstWide-DistinguishedNamingInOutput'

repadmin /kcc <DCrunfrom>
#It will trigger the kcc to run and and recalulate replication settings between the DC's. it is not really needed to run this command, you can also wait because the kcc will run automatically at set intervals.
```

## The global catalog partition
- only available on Domain controllers that have the 'Global Catalog' Function
- This partition is replicated to every Global Catalog inside the forest.
- In deze partition wordt een mini- versie van de domain partition bewaard. De Global Catalog partition bevat niet alle attributen van objecten die in de domain partition staan.

De global catalog partition zal van alle users, computers, en andere object in de domain partition die gegevens opnemen die :

- Uniek zijn, (bvb. Een username is een unieke naam, en is handig voor search doeleinden)

- Statisch zijn (bvb. De geboordtedatum van een user nemen we in de GC partition op omdat het een goed criterium is voor een search, en omdat het nooit kan veranderen)

- En nuttig zijn voor een search opdracht (een paswoord is dan wel uniek, maar verandert constant, en het heeft geen zin om dit bij te houden, want we doen nooit een zoekopdracht naar een user die een bepaald paswoord heeft)

- Op deze manier beschikken we over een gereduceerde versie van de domain partition waarin we snel naar nuttige informative kunnen zoeken. Andere domains en domain controllers kunnen op die manier informatie op een snelle manier in het forest terug vinden.