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
! DHCP configuration
! -----------------
ip dhcp excluded-address <begin_addr> <end_addr>
ip dhcp pool <pool_name>
network <network_id> <subnetmask>
default-router <def_gateway_ip>
dns-server <dns_ip>
!
! Static routes
! -------------
! ip route 0.0.0.0 0.0.0.0 <next_hop_router>
! 
! VLAN configuration
! ------------------
interface GigabitEthernet0/0/0.10
encapsulation dot1Q 10
ip address <ip_addr> <submask>
!
! OSPF general configuration
! --------------------------
router ospf <processID
router-id <x.x.x.x>
passive-interface <interface_name>
auto-cost reference-bandwidth <ref_BW_Mbps>
network 192.168.1.0 0.0.0.255 area 0
network 192.168.0.0 0.0.0.3 area 0
default-information originate
!
! OSPF interface configuration
! ----------------------------
interface <interface_name>
ip ospf 10 area 0
ip ospf network point-to-point area 0
ip ospf cost 500
ip ospf priority 77
ip ospf hello-interval <seconds>
ip ospf dead-interval <seconds>
!
! Standard numbered ACL
! ---------------------
access-list <1-99> remark <remarkontheacl>
access-list <1-99> permit <source_subnet> <source wildcard>
access-list <1-99> permit host <source_host_IP>
!
! standard named ACL
! ------------------
ip access-list standard <nameoftheacl>
remark <remark>
permit <source_subnet> <wildcardmask>
permit any
permit host <source_host_IP>
!
! Extended numbered ACL
! ---------------------
access-list <100-199> permit ip <source_subn> <wildcard> <dest_subn> <wildcard>
access-list <100-199> permit tcp <source> <destination> eq <port#>
!
! Extended named ACL
! ---------------------
ip access-list extended <nameofextendedACL>
remark <remark>
permit ip any any
permit ip <source_subnet> <wildcard> <destination_subnet> <wildcard>
permit tcp any any eq <tcp_port_#>
!

```