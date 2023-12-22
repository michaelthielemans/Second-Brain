#cisco #switching #networking 

# STP algoritm process

1. elect root bridge
2. elect root ports
3. elect designated ports
4. elect alternate ports

# BPDU packets

|priority|extended system ID | MAC | root ID | root path cost|
|--|--|--|--|--|

# stp types:

| STP types | -- |
|--|--|
|STP | spanning tree|
|PVST | PerVlan spanning tree|
|RSTP | rapid spanning tree
|PVST+ | PerVlan Spanning tree enhanced|




# Port fast on a switchport

configure 'portfast ' on a switchport if you want to skip the stp protocol states (15s +15s) and put the port immediately in forwarding mode. This is only advisable on switchports connected to a host and not to another switch.

# BPDU - guard

This is a protection mechanism when a port is configured as a portFast. If the port receives a BPDU message (which can only happen when another switch is connected to that port) the port will be put immediately in a error-disabled state. This prevents misconfiguration.