#cisco #switching #networking
# Vlans
Vlan ID 1 - 1005 = saved in flash : vlan.dat
vlanid 1006 - 4094 = saved in running-config

>[!attention] delete all vlans at once -> delete flash: vlan.dat
>

## configure SVI -  Switch virtual Interface
```
(conf)#interface vlan 99
(conf-if)#ip address x.x.x.x x.x.x.x

```
## configure access vlan
`(conf-if)#switchport mode access`
`(conf-if)#switchport access vlan xxx```

## Show commands for vlans

```
show vlan brief
show vlan summary
show vlan <ID>
```

# Trunks

## configure a trunk on switch
```
(conf-if)# switchport mode trunk
(conf-if)# switchport trunk native vlan <ID>
(conf-if)# switchport trunk allowed vlan <ID>
```

```
check the config
#show interface fa 0/18 switchport
```
## configure a trunk on a router

```

R1(conf)#interface g0/1.10
R1(conf-if)#encapsulation dot1q vlan 10
R1(conf)
```

## DTP - Dynamic Trunking Protocol
is cisco proprietary protocol
>[!attention] DTP is not secure

### Configure DTP

```
disable DTP on the trunk:
(conf-if)# switchport nonegotiate

enable DTP on the trunk:
(conf-if)# switchport dynamic auto (-> follows neigbour)
(conf-if)# switchport dynamic desirable (-> actively tries to be a trunk)
```

### show DTP
`show dtp interface fa 0/1`


