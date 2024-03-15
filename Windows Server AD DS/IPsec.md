certificates are used for
- IIS HTTPS
- IPSEC
- L2TP


## IPSEC on windows computer

mmc.exe -> add snap-in : IP security policy management
1. create ip security policy
2. name for example -> very secure ping
3. no activate default rules ( if the default rules are selected -> this will use kerberos)
4. add rule
	1. does not specify tunnel
	2. lan
	3. ip filter list -> add (= filtering WHEN the policy is applied)
		1. new filter name
		2. my ip address =  choose source ip address
		3. a specific address -> ip of counterpart
		4. select ICMP
	4. filter action
		1. new name
		2. negotiate security
		3. do not allow
		4. integrity (is it spoofed) + encrypt. , 
	5. auth method
		1. select the tools to do the 
		2. use preshared key - the same key need to be used on both ends.
		3. kerberos = username + passw like AD, voor kerberos ath you always need a good connection to the domain controllers TGS