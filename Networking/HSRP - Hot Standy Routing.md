#cisco #networking 

# Concept

Multiple firsthop routers can act as one default gateway. On of the routers will be the active and the other will be the standby router who will take over the role of the active if the active routers fails.
# HSRP priority

- 2 routers configured with HSRP will start an election process.
- The router with the highest HSRP priority will become the active router.
- By default, the HSRP priority is 100.
- If the priorities are equal, the router with the numerically highest IPv4 address is elected as the active router.
```
standby priority <0-255>
```

## HSRP Preemption

By default, if a router becomes the active router, it will remain the active router even if another router comes online with a higher HSRP priority.

- To force a new HSRP election process to take place when a higher priority router comes online, preemption must be enabled using the **standby preempt** interface command.
- Preemption is the ability of an HSRP router to trigger the re-election process. With preemption enabled, a router that comes online with a higher HSRP priority will assume the role of the active router.
- Preemption only allows a router to become the active router if it has a higher priority. A router enabled for preemption, with equal priority but a higher IPv4 address will not preempt an active router.
# HSRP States and Timers

|HSRP State|Description|
|---|---|
|Initial|This state is entered through a configuration change or when an interface first becomes available.|
|Learn|The router has not determined the virtual IP address and has not yet seen a hello message from the active router. In this state, the router waits to hear from the active router.|
|Listen|The router knows the virtual IP address, but the router is neither the active router nor the standby router. It listens for hello messages from those routers.|
|Speak|The router sends periodic hello messages and actively participates in the election of the active and/or standby router.|
|Standby|The router is a candidate to become the next active router and sends periodic hello messages.|
|Active|The router won the election.|

# configuration
The configuration of HSRP will all happen on the selected interface.
1. go to the interface
2. make the interface HSRP aware  `standy <group-id> ip <virtual_ip>`
3. (optionaly) Set priority  `standby <group-id> priority <0-255>`
4. (optionaly) The interface that has preempt enabled will actively push the election process even if the other routers interface does not have preempt enabled.  `standby <group-id> preempt`

```
R1(config-if)# standby 1 ip 192.168.1.254
R1(config-if)# standby 1 priority 150
R1(config-if)# standby 1 preempt
```

## show commands
```
R1# show standby
R1# show standby brief
```