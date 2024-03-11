#ActiveDirectory 
# intra site replication
every 5 min a DC will NOTIFY the other DCs if he has changes in its database
these properties are in the registry
-> he will not SEND the updates himself
If the amount of updates is large it can happen that the DC sends a notify faster than 5 minutes.

replication protocol = RPC
RPC works with dynamic ports. Is not firewall friendly


Replication can happen every moment of the day

every hour 1 DC will contact the other to ask for changes -> PULL REPLICATION


# inter site replication

- every 3hours dc will contact the others to ask for changes
- no notify -> no push replication
- Protocol for replication = IP   => firewall friendly
- can happen dat and night, as long as the dc waits for 2 hours before a new pull attempt is started.


# Moving a dc from a local site to a remote site
If you move the DC all the configuration for replication happen automatically, If it fails CHECK DNS !!
There is a service(KCC= knowledge consistency checker) that checks every 15 min the site structure and configure automatically the best configuration

If the connectin object is not created automatically by the KCC , than best check the DNS settings.

You can manually trigger the KCC,  rightclick NTDS settings -> all tasks -> check replication topology

so behind the NTDS object sits the KCC that configures the stuff.

# Manually trigger replicate

1. With AD sites and services console
	1. NTDS -> rigth click on the connection object
2. via command line -> PS# repadm /replicate

# check replication status
1. PS# repadmin /showrepl
2. AD replications tool => need to be installed separately.

If replications fails (happens when a new dc is added) the KCC has maybe not yet run , so the new settings are not added yet
-> do a 'check replication topology'


# Adding new connection objects is not advised.


# Which data will be replicated
1. domain partition
2. schema partition
3. dns zones


# steps for creating new site

1. create a new subnet
2. create a new site and assign the correct subnet
3. move the domain controller object to the new site
4. force a check replication topology on NTDS objects
5. check replication / force a replication
6. check the settings of the NTDS connection object
	1. -> schedule, protocol