
#cisco #routing #ospf
> [!info] link-state = Information about the network prefix, prefix length, and cost

## OSPF  architecture (high level)

>[!success] Routing protocol messages

>[!success] Building data structure = DataBase

>[!success] calculating algorithm = Dijkstra

## Link-State Operation steps
Each router in the OSPF network is processing through the following steps:

1. Establish Neighbour Adjacencies = Hello packets
2. Exchange Link-State Advertisements = LSA's
3. Build the Link State Database
4. Execute the SPF Algorithm -> generate an SPF tree -> runs after every database update
5. Choose the Best Route -> calculated routes are added to the routing table

## OSPF packets

### OSPF routing protocol messages 

| version | type

| type| packet | short | description |
|-|-|-|-|
| 1| Hello packet | - | Discovers neighbors and builds adjacencies between them, establishing and maintaining adjacency |
|2|Database description packet | DBD | Checks for database synchronization between routers, this packet contains an abbreviated list of the sending router LSDB|
|3|Link-state request packet | LSR | Requests specific link-state records from router to router |
|4|Link-state update packet | LSU | Sends specifically requested link-state records, these consists of 7 different types of LSA's |
|5|Link-state acknowledgment packet | LSAck | Acknowledges the other packet types, except HELLO packets

### Link State Advertisement (LSA) packets within the LSU 's

| lsa type|description|
|-|-|
|1|router lsa's|
|2|database sync between routers|
|3-4|summary lsa's|
|5| autonomous system external lsa's
|6| acknowledges the other packet types
|7| defined for not-so-stubby areas
|8| external attributes for border gateway protocol (bgp)
|9| intra-area lsa's



### Hello packets

## OSPF Databases

| Database | table | description | command |
| -- | -- | -- | -- |
| Adjacency Database|Neighbor Table| <ul><li>Neighbor routers with bi-directional connect</li><li>table = Unique for each router</li></ul>| `show ip ospf neighbor network` | 
| Link-state Database (LSDB) | Topology Table | <ul><li>This database represents the network LSDB</li><li>All routers within an area have identical LSDB</li></ul> | `show ip ospf database` |
| Forward database | routing table | <ul><li>List of routes generated when an algorithm is run on the link-state database</li><li>Each router's routing table is unique and contains information on how and where to send packets to other routers</li></ul>| `show ip route`| 

## OSPF Areas

* **single-area** -> all routers within area 0
* **multi-area** -> backbone network stays at area 0

>	The routing domain is divided into multiple smaller routing domains 
>	will produce smaller routing tables
>	reduced link-state updates
>	less frequent SPF calculations

### OSPFv3 = OSPFv2 for IPv6


## OSPF Operational States
>
| state | description  |
|---|---|
|Down State|<li>No Hello packets received = Down</li><li>Router sends Hello packetsTransition to Init state</li>|
|Init State|<li>Hello packets are received from the neighbor</li><li>They contain the Router ID of the sending router Transition to Two-Way state.</li>|
|Two-Way State|<li>In this state, communication between the two routers is bidirectional</li><li>On multiaccess links, the routers elect a DR and a BDR.Transition to ExStart state</li>|
|ExStart State|On point-to-point networks, the two routers decide which router will initiate the DBD packet exchange and decide upon the initial DBD packet sequence number.|
|Exchange State|<li>Routers exchange DBD packets</li><li>If additional router information is required then transition to Loading; otherwise, transition to the Full state.</li>|
|Loading State|<li>LSRs and LSUs are used to gain additional route information</li><li>Routes are processed using the SPF algorithm</li><li>Transition to the Full state.</li>|
|Full State|The link-state database of the router is fully synchronized.|


### Database sync


## OSPFv3 = OSPF for ipv6
# command line

show commands
>| `show ip protocols | include Router ID` |
>|-|-|
>|`R1# show ip ospf interface GigabitEthernet 0/0/0`| ospf interface information|

ospf config commands
>
|command| description|
| - | -|
| `router ospf 10`| start osp process-id 10 |
|`R1(config-router)# router-id 1.1.1.1`| assign a router id|
|`R1# clear ip ospf process`| clear all ospf configuration |
| `network 10.10.1.0 0.0.0.255 area 0`| adding area's|
|`R1(config-if)# ip ospf 10 area 0`| configure ospf on the selected interface|

