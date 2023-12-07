#cisco #routing #ospf

> [!info] link-state = Information about the network prefix, prefix length, and cost
ospf is an IGP - Interior Gateway Protocol
## OSPF  architecture (high level)

>1. Routing protocol messages
>2. Building data structure = DataBase
>3. Calculating algorithm = Dijkstra -> add new routes to the routing table
### Link-State Operation steps
Each router in the OSPF network is processing through the following steps:

1. Establish Neighbour Adjacencies = Hello packets
2. Exchange Link-State Advertisements = LSA's
3. Build the Link State Database
4. Execute the SPF Algorithm -> generate an SPF tree -> runs after every database update
5. Choose the Best Route -> calculated routes are added to the routing table

## OSPF Operational States
### Down state
- This is the state when OSPF is just enabled on a port but haven't send or received a hallo packet jet.

### Init Start state
- A multicast Hello packet is send to, or received from the neighbour.
- Those packets contain the Router ID of the sending router and optionally a list with all the other routerID of neighbours he already knows.
```mermaid
sequenceDiagram
participant RouterA
participant RouterB
	RouterA-)+RouterB: Hello multicast packet
	RouterB--)+RouterA: unicast answer to hello packet
```

### Two-way state:
1. This state starts from the moment that the router sees his own routerID in the answer packet he received from his neighbour router.
2. The communication between the two routers is bidirectional. This means that the router has received an answer to his multicast hello packet.
3. The router adds the neighbour to his database
4. On multi-access links the DR and a BDR election starts.
5. The router with the highest priority or the highest router ID will be chosen as the DR, the second highest is the BDR (backup Designated Router)
6. DROTHER routers will stay in this 2-way state ( = an adjacency with the DR)
```mermaid
sequenceDiagram
participant RouterA
participant RouterB
Note over RouterA,RouterB: when seeing their own routerID in the answer packet
RouterA--)RouterA:Start DR election process
RouterB--)RouterB:Start DR election process
Note over RouterA,RouterB: Highest priority or else highest routerID => DR ->BDR
```
### Exstart state
- On point-to-point networks, the two routers decide which router will initiate the DBD packet exchange. The router with the highest routerID will send its DBD first and decide upon the initial DBD packet sequence number.
### Exchange State
- This state starts when the first DBD packet is send or received. 
- Routers exchange DBD packets. ==The DBD (database description) is a summarised form of the LSDB (Link State Database)==
- On multi-access networks, DBD packets will only be transfered with the DR
- If additional router information is required then transition to Loading; otherwise, transition to the Full state
```mermaid
sequenceDiagram
participant RouterA
participant RouterB
Note over RouterA,RouterB: router with highest routerID start sending DBD
	RouterB-)RouterA: send DBD
	RouterA--)RouterB: LSAck
	RouterA-)RouterB: send DBD
	RouterB--)RouterA:LSAck
```


### Loading state
1. If the router sees a more current link-state entry in the DBD he just received from his neighbour, the router will transition to the loading state by sending a LSR (link state request).
2. LSR (Links state request) and LSU (Link state update) are used to gain additional route information
```mermaid
sequenceDiagram
participant RouterA
participant RouterB
RouterB-)RouterA:Send LSR
RouterA-)RouterB:Send LSU
RouterB--)RouterA:send LSAck
```

When a change is perceived (incremental updates)
### Full state
- The link-state database of the router is fully synchronized. LSU's are send when a change is perceived (incremental updates), or every 30min
- Routes are processed using the SPF algorithm



To verify the OSPFv2 adjacencies, use the `show ip ospf neighbor` command. The state of neighbors in multiaccess networks can be as follows:

>FULL/DROTHER - This is a DR or BDR router that is fully adjacent with a non-DR or BDR router. These two neighbors can exchange Hello packets, updates, queries, replies, and acknowledgments.

>FULL/DR - The router is fully adjacent with the indicated DR neighbor. These two neighbors can exchange Hello packets, updates, queries, replies, and acknowledgments.

>FULL/BDR - The router is fully adjacent with the indicated BDR neighbor. These two neighbors can exchange Hello packets, updates, queries, replies, and acknowledgments.

>2-WAY/DROTHER - The non-DR or BDR router has a neighbor relationship with another non-DR or BDR router. These two neighbors exchange Hello packets.

The normal state for an OSPF router is usually FULL. If a router is stuck in another state, it is an indication that there are problems in forming adjacencies. The only exception to this is the 2-WAY state, which is normal in a multiaccess broadcast network


## OSPF Packets

| type| packet | short | description |
|-|-|-|-|
| 1| Hello packet | - | Discovers neighbors and builds adjacencies between them, ==establishing== and ==maintaining== adjacency. |
|2|Database description packet | DBD | This packet contains an abbreviated list of the sending router LSDB, it contains all the header LSU information|
|3|Link-state request packet | LSR | Requests more link-state information about an entry in his LSDB|
|4|Link-state update packet | LSU | Sends a reply on requested link-state records or send new updates, these consists of 7 different types of LSA's |
|5|Link-state acknowledgment packet | LSAck | Acknowledges any other OSPF packet type, except HELLO packets

### Hello packets in detail
> - The Hello packets are send to multicast address 224.0.0.5
> - Content of a hello :
> 	- The routers own routerID
> 	- A list of all the routerID's of his neighbours. (if he has already neighbours)
> 	- A request, 'Is there anyone else on the link?'
> - by default hello packets are send every 10sec on a ethernet link and 30 sec on a ptp link

> - Answer to hello packet are send as unicast messages and also contains a list of all the neigbours that the sending router knows. So if the receiving routers sees his own routerID in the reply then he knows that they both know each other.

#### Death interval
- Is the interval in seconds that a ospf interface waits before it will notice that the adjacency with its neighbor is down
	- 4 times the hello interval by default.
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




## OSPF Databases

| Database | table | description | command |
| -- | -- | -- | -- |
| Adjacency Database|Neighbor Table| <ul><li>Neighbor routers with bi-directional connection</li><li>table = Unique for each router</li></ul>| `show ip ospf neighbor network` | 
| Link-state Database (LSDB) | Topology Table | <ul><li>This database represents the network LSDB</li><li>All routers within an area have identical LSDB</li></ul> | `show ip ospf database` |
| Forward database | routing table | <ul><li>List of routes generated when an algorithm is run on the link-state database</li><li>Each router's routing table is unique and contains information on how and where to send packets to other routers</li></ul>| `show ip route`| 

## OSPF Areas

* **single-area** -> all routers within area 0
* **multi-area** -> backbone network stays at area 0

>- The routing domain is divided into multiple smaller routing domains 
>- will produce smaller routing tables
>- reduced link-state updates
>- less frequent SPF calculations

## Wildcard mask calculation
> Wildcard mask = 255.255.255.255 - subnetmask
> 255.255.255.0 -> 0.0.0.255
## OSPFv3 = OSPF for ipv6
## Router ID selection

> All routers in the ospf area must have a routerID. If not manually entered a routerID is chosen automatically.

Manually configure a router ID -> `router-id 1.1.1.1` [[#Configure a RouterID]]
Automatically assign router ID 

```mermaid
flowchart TD

A[routerID explicit configured?] -->|No| B[IP loopback interface configured?]
A-->|yes| D(Use the routerID)
B-->|no| C(Use the highest active IP interface configured)
B-->|yes| D
```

#### Use loopback as the routerID
>Instead of relying on physical interface, the router ID can be assigned to a loopback interface. Typically, the IPv4 address for this type of loopback interface should be configured using a 32-bit subnet mask (255.255.255.255). This effectively creates a host route. A 32-bit host route would not get advertised as a route to other OSPF routers

>[!attention] Be aware that you have to reset the ospf process after you modified the router-id.
>[[#Change the Router-ID]]



## DR and BDR

### Why do we need a DR / BDR
A multi-access network (multiple routers on one single subnet - L2 net) can have 2 problems:
- An extensive amount of adjacencies
- An enormous amount of LSA flooding over the network (multicast)

>[!info] If there would be no DR and BDR election:
>Calculate the total amount of adjacencies on a multi-access network:
>n= number of routers in the network
>total amount of adjacencies = n(n-1) / 2

>Without a DR and BDR all the LSU messages would be flooded on the network. Also the amount of LSAck packets could become enormous. This is because every flooded (multicast) LSU packet has to be acknowledged by every router.

>OSPF elects a DR to be the collection and distribution point for LSAs sent and received. A BDR is also elected in case the DR fails. All other routers become DROTHERs. A DROTHER is a router that is neither the DR nor the BDR.

### DR and BDR election process

1. Router with highest priority is chosen as DR. (default priority = '1')
2. Router with highest routerID is chosen as DR
3. Router with a priority '0' will not take part in the election process.
4. A value of 0 does not become a DR or a BDR.
5. A value of 1 to 255 on the interface makes it more likely that the router becomes the DR or the BDR.

![[Pasted image 20231130140530.png]]

#### Procedure when DR fails!
>If the DR fails, the BDR is automatically promoted to DR. This is the case even if another DROTHER with a higher priority or router ID is added to the network after the initial DR/BDR election. However, after a BDR is promoted to DR, a new BDR election occurs and the DROTHER with the highest priority or router ID is elected as the new BDR.




### Change OSPF interface priority
[[#Change router priority]]
>[!attention] After changing the router priority you have to reset the ospf process.
### How the DR send updates to its ospf neighbor routers
The DR is responsible for collecting and distributing LSAs sent and received. The DR uses the multicast IPv4 address 224.0.0.5 which is meant for all OSPF routers.
### BDR functions
- The BDR listens passively and maintains a relationship with all the routers. If the DR stops producing Hello packets, the BDR promotes itself and assumes the role of DR. Like the DR he also listens on the multicast address (244.0.0.6) for incoming ospf packets.
### DROTHERS
- All other routers become a DROTHER (a router that is neither the DR nor the BDR). DROTHERs use the multiaccess address 224.0.0.6 (all designated routers) to send OSPF packets to the DR and BDR. Only the DR and BDR listen for 224.0.0.6.
### Passive interfaces
By default, OSPF messages are forwarded out all OSPF-enabled interfaces. However, these messages only need to be sent out interfaces that are connecting to other OSPF-enabled routers.
Sending out unneeded messages on a LAN affects the network in three ways:
- Inefficient Use of Bandwidth - Available bandwidth is consumed transporting unnecessary messages.
- Inefficient Use of Resources - All devices on the LAN must process and eventually discard the message.
- Increased Security Risk - Without additional OSPF security configurations, OSPF messages can be intercepted with packet sniffing software. Routing updates can be modified and sent back to the router, corrupting the routing table with false metrics that misdirect traffic.
[[#Configure a Passive Interface]]
### Point-to-point links
By default, Cisco routers elect a DR and BDR on Ethernet interfaces, even if there is only one other device on the link. You can verify this with the show ip ospf interface command. The DR/ BDR election process is unnecessary as there can only be two routers on the point-to-point network between R1 and R2. Notice in the output that the router has designated the network type as BROADCAST.
[[#Point-to-point links]]
## Cost calculations & adjustments

- In ospf the Metric of a route is called the cost.
- The lower the cost the better
- reference bandwidth by default = 100,000kbps = 100Mbit
- Lowest cost = 1 (only integer values)

Cost calculation = reference bandwidth / interface bandwidth

>[!attention] If you change the reference bandwidth, you have to change it on ALL routers!!

### Default Route Propagation
if a default static route is configured on an interface it is possible to propagate this route into OSPF 
for example, the static route: ip route 0.0.0.0 0.0.0.0 <next-hop-address | exit-intf>
```
R2(config)# router ospf 10
R2(config-router)# default-information originate
```
----

---------
## OSPF Configuration
### NEW OSPF process
Start a new ospf process with a specific process ID. It is not necessary to use the same process id on all the routers in the same ospf area, but is is recommended.
```cisco
R1(conf)router ospf 10
```
### Configure a Router-ID
```
R1(conf)router ospf 10
R1(conf-router)router-id 1.1.1.1
```
#### Change the Router-ID
```
R1(conf)router ospf 10
R1(conf-router)router-id 2.2.2.2
R1#clear ip ospf process
```
### Modify router priority

```
R1(conf)#interface fa0/1
R1(conf-if)#ip ospf priority 50
R1#clear ip ospf process
```


### Check if the interface = DR/BDR/DROTHER
```
show ip ospf interface fa0/1
```
### Verify DR/BDR Adjacencies
you can see all the neighbor routers and the state of the adjacency
```
show ip ospf neighbor
```
### Adding networks to the OSPF process

1. In the first example, the wildcard mask identifies the interface based on the network addresses. Any active interface that is configured with an IPv4 address belonging to that network will participate in the OSPFv2 routing process.
```
R1(config)#router ospf 10
R1(config-router)#network 10.10.1.0 0.0.0.255 area 0
R1(config-router)#network 10.1.1.4 0.0.0.3 area 0
R1(config-router)#network 10.1.1.12 0.0.0.3 area 0
```

2. As an alternative, the second example shows how OSPFv2 can be enabled by specifying the exact interface IPv4 address using a quad zero wildcard mask. Entering **network 10.1.1.5 0.0.0.0 area 0** on R1 tells the router to enable interface Gigabit Ethernet 0/0/0 for the routing process. As a result, the OSPFv2 process will advertise the network that is on this interface (10.1.1.4/30).
```
R1(config)#router ospf 10
R1(config-router)#network 10.10.1.1 0.0.0.0 area 0
R1(config-router)#network 10.1.1.5 0.0.0.0 area 0
R1(config-router)#network 10.1.1.14 0.0.0.0 area 0
```

### Configure OSPF  from the interface, using the ip ospf Command
```
R1(config)#interface GigabitEthernet 0/0/0
R1(config-if)#ip ospf 10 area 0
```
### Configure a Passive Interface
>Use the **passive-interface** router configuration mode command to prevent the transmission of routing messages through a router interface, but still allow that network to be advertised to other routers. The configuration example identifies the R1 Loopback 0/0/0 interface as passive.
```
R1(config-router)#passive-interface loopback 0
```
### Configure a point-to-point link (on multi-access link)
```
R1(conf)#interface fa0/1
R1(conf-if)#ip ospf network point-to-point
```


----
### Modify the reference bandwidth (cost reference)
```
R1(conf)auto-cost reference-bandwidth <value in Mbps>
```
### Manually change cost on interface
```
R1(conf-if)#ip ospf cost <cost value>
```
### Modify hello and dead intervals
```
Router(config-if)# ip ospf hello-interval <seconds>
Router(config-if)# ip ospf dead-interval <seconds>
```
#### Set the hello and dead intervals to default values
```
R1(conf-if)#no ip ospf hello-interval
R1(conf-if)#no ip ospf dead-interval
```

### Default static route propagation
```
R2(config)#router ospf 10
R2(config-router)# default-information originate
```
## All OSPF Commands

#### show commands:
```
R1#show ip ospf neighbor
show ip protocols
show ip ospf
show ip ospf interface
```

#### ospf config commands


|command| description|
| -- | -- |
|`R1(conf)# router ospf 10`| start osp process-id 10 |
|`R1(config-router)# router-id 1.1.1.1`| assign a router id|
|`R1#clear ip ospf process`| reload the new ospf configuration |
|`Router(config-router)#network 10.10.1.0 0.0.0.255 area 0`| adding area's|
|`R1(config-if)# ip ospf 10 area 0`| configure ospf on the selected interface|
|`R1(config-router)#passive-interface loopback 0` | make passive interface|
|`R1(config-router)#auto-cost reference-bandwidth`|--|
```
R1(conf)#router ospf 56
R1(conf-router)#default-information originate
```
#### debug hello packets , adjacencies
debug ip ospf adj




disable all debugging
`no debug all

