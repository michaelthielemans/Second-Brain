#cisco #config 
```
! General config
! --------------
hostname R2
username cisco secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
ip domain-name <domain.ext>
no ip domain-lookup
!
banner motd <message>
!
line con 0
password class
login local
!
line vty 5 15
login local
transport input ssh
!
ip ssh version 2
!
! VLAN
! -----
vlan 10
interface vlan 10
name <name_of_vlan>
interface vlan 10
no shut

!
ip default-gateway <ip addr>
```
