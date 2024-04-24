#ActiveDirectory 
# Replication between DC’s in 1 site

- Every hour 1 DC will contact the others to ASK for changes (PULL REPLICATION)  
- Every 5 minutes 1 DC will NOTIFY the other DC’s of the changes in its database (PUSH REPLICATION) 
- If the amount of updates is large it can happen that the DC sends a notify faster than 5 minutes.
- The protocol for replication is RPC (remote procedure calls) 
	RPC works with dynamic ports. Is not firewall friendly
- Replication can happen every moment of the day (no schedule)
	It is not possible to configure a schedule
# AD replication between DCs of OTHER sites

- Every 3 hours dc will contact the others to ask for changes (pull request)
- The DC has 1 hour to continue replication.
- There is no notify -> no push replication only pull
- Protocol for replication = IP with fixed port  => firewall friendly
- Can happen day and night, as long as the dc waits for 2 hours before a new pull attempt is started. Time frames can be configure.

# KCC -Knowledge Consistency Checker- service

The KCC service task is to create the 'automatically generated' connection object.
Based of the structure of your sites it will auto configure. 

KCC checks every 15 min the site structure and configure automatically the best configuration

You can manually trigger the KCC,  right-click NTDS settings -> all tasks -> check replication topology

Open 'Sites and Services' select the "NTDS settings" of the DC you want to generate automatically the connection object, right-click on "NTDS settings" and select "check replication topology". do the same on the other DCs if needed.

Once you create a connection object yourself the KCC will not be responsible and thus it will not be updated
# Moving a dc from a local site to a remote site
If you move the DC all the configuration for replication happen automatically, If it fails CHECK DNS !!

If the connection object is not created automatically by the KCC , than best check the DNS settings.

You can manually trigger the KCC,  right-click NTDS settings -> all tasks -> check replication topology

so behind the NTDS object sits the KCC that configures the stuff.

# Manually trigger replicate or force a replication

1. With AD sites and services console
	1. NTDS -> right-click on the connection object -> replicate now
		this is a one-way replication, it is a pull request. If you want to replicate in 2-way, you also have to do the same on the other DC.
1. via command line -> PS# repadm /replicate

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