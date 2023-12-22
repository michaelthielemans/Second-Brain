#cisco #management
## cdp cisco discovery protocol

layer 2 protocol
CDP advertisements
enabled by default , can be disabled -> `no cdp enable
only on cisco device
disable globally `no cdp run

#### Parameters that are exchanged
>- name of the device
>- number and type of interfaces
>- type of device

```
show cdp neigbors
show cdp neighbors detail
```
## lldp

- not proprietary to cisco, used by many vendors, vendor-neutral protocol
- disabled by default on cisco

enable globaly: `lldp run`

enable on a interface
```
lldp transmit
lldp receive
```
## ntp - network time protocol

- ntp uses udp port 123i

Sync the device to a ntp server
```
ntp server 209.165.200.225
show clock detail
show ntp associations
```

## Hierarchical  structure

stratum 0 = the clock source itself (atomic clock,...)
stratum 1 = first server that receives this clock
stratum 2 = the second server that syncs to a stratum 1
[[NTP.excalidraw]]

## snmp

simple network management protocol

snmp manager = the monitoring system (zabbix)
snmp agent = catches the information and sends it to zabbix, it will look inside the MIB the value
MIB : management Information Base

snmp get
snmp set

### snmp versions

snmpv3
authentication and encryption


#### snmp traps
>configured on the device itself
>when a threshold is hit a snmp message is send to a specified snmp manager

### MIB
OID = object ID

### cisco object coordinatior

## syslog

- uses port 514

cisco devices sending its logs to a central syslog server

- logging buffer

## router file systems
```
show file systems
dir
cd nvram:

```

location of the startup config = nvram:

location of the IOS bin file = flash

## TFTP

```
copy running-config tftp

.....
.....


copy tftp running-config
copy tftp <name of a config file>
```


## USB connectivity on devices

```
copy running-config usbflash:/
more usbflash:/R1-config
```
usb has to be in filesystem format fat32

read a file on nvram directly
`more <filename>`


