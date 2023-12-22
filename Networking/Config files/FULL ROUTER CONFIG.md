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
! VLAN configuration on router
! ----------------------------
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
! ------------------
ip access-list extended <nameofextendedACL>
remark <remark>
permit ip any any
permit ip <source_subnet> <wildcard> <destination_subnet> <wildcard>
permit tcp any any eq <tcp_port_#>
exit
!





! GRE Tunnel (ipv4)
! ----------
interface tunnel 0
ip address <tunnel ip source>
tunnel source <loopback 0>
tunnel destination <ip of destination>
bandwidth <bw in kb>
ip mtu <1400 - in bytes>
exit
!
! GRE tunnel (ipv6)
! -----------------
interface tunnel 0
ip address <tunnel interface IP>
tunnel source <mostly loopback o>
tunnel destination <ip of dest>
tunnel mode gre ipv6
exit
!
! IPSEC tunnel
! ------------
crypto isakmp policy 10
encryption aes 256
hash sha256
authentication pre-share
group 14
lifetime 3600
exit
!
crypto isakmp key <pre-shared key> address <remote peer ip>
!
crypto ipsec transform-set GRE-VPN esp-aes 256 esp-sha256-hmac
mode transport
exit
!
! create crypto map
! -----------------
crypto map GRE-CMAP 10 ipsec-isakmp
match address GRE-VPN-ACL
set transform-set <transform-set-name>
set peer 64.100.1.2
exit
!
! assign the map to an interface
! ------------------------------
interface g0/0/0
crypto map GRE-CMAP
!
! create IPsec profile
! ----------------
crypto ipsec profile <profile_name>
set transform-set <transform-set-name>
exit
!
! apply the profile to an interface
! ---------------------------------
interface tunnel 1
tunnel protection ipsec profile <profile_name>
```