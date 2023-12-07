## VPN types

### Enterprise and service provider VPNs

>Enterprise VPNs
- Common solution for securing enterprise traffic across the internet
- Site-to-site and remote access VPNs are created and managed by the enterprise using IPsec and SSL VPNs.

>Service Provider VPNs
- created and managed by the provider network.
- Multiprotocol Label Switching (MPLS) at Layer 2 or Layer 3
- Create secure channels between an enterprise’s sites, effectively segregating the traffic from other customer traffic.
### Remote access VPNs
- Clientless VPN connection
	The connection is secured using a web browser SSL connection.

- Client-based VPN connection
	VPN client software such as Cisco AnyConnect Secure Mobility Client must be installed on the remote user’s end device.
### Site-to-site VPNs

## SSL VPNs
SSL uses the public key infrastructure and digital certificates to authenticate peers. The type of VPN method implemented is based on the access requirements of the users and the organization’s IT processes. The table compares IPsec and SSL remote access deployments

## GRE over IPsec
- Generic Routing Encapsulation (GRE) is a non-secure site-to-site VPN tunneling protocol.
- A GRE tunnel can encapsulate various network layer protocols as well as multicast and broadcast traffic.
- GRE does not by default support encryption; and therefore, it does not provide a secure VPN tunnel.
- A GRE packet can be encapsulated into an IPsec packet to forward it securely to the destination VPN gateway.
- Standard IPsec VPNs (non-GRE) can only create secure tunnels for unicast traffic.
- Encapsulating GRE into IPsec allows multicast routing protocol updates to be secured through a VPN.

The terms used to describe the encapsulation of GRE over IPsec tunnel are passenger protocol, carrier protocol, and transport protocol.

- Passenger protocol – This is the original packet that is to be encapsulated by GRE. It could be an IPv4 or IPv6 packet, a routing update, and more.

- Carrier protocol – GRE is the carrier protocol that encapsulates the original passenger packet.

- Transport protocol – This is the protocol that will actually be used to forward the packet. This could be IPv4 or IPv6.

## GRE tunnel configuration

1. Create the tunnel interface by using the global configuration command interface tunnel tunnel-number.
2. Identify the local source of the tunnel by using the interface parameter command tunnel source {ip-address | interface-id}. The tunnel source can be a physical interface or a loopback interface.

Step 3.  Identify the remote destination IP address by using the interface parameter command tunnel destination ip-address.

Step 4.  Allocate an IP address to the tunnel interface by using the command ip address ip-address subnet-mask.

# IPsec technologies

|IPsec| protocols |
|--|--|--|
|IPsec header|
|confidentiality| DES, 3DES, AES, SEAL| symmetric keys|
|integrity|HMAC(MD5, SHA)|check data not changed in transit|
|authentication|Pre-shared key (PSK) or (RSA) authentication uses digital certificates|
|Diffie-Helman|

# IKE - Internet Key Exchange Phases

Phase 1: negotiation of the policy set =  mgmt, 1 set
	1. encryption
	2. hashing : MD5, SHA, HMAC(hashed M authentication Code= keyed hash)
	3. auth method: pre-shared key , public key, X.509(certificate)
	4. Diffie-Hellman group
Phase 2: Negotiates the transform set = DATA, 2 sets ( 1 inbound + 1 outbound)
	1. encryption: esp-aes 256
	2. hashing: esp-sha
# IPsec tunnel / transport mode
Traditional IPsec provides two modes of packet transport:

1. Tunnel mode
	Encrypts the entire original packet and adds a new set of IPsec headers.  These new headers are used to route the packet and also provide overlay functions.
	
2. Transport mode
	Encrypts and authenticates only the packet payload. This mode does not provide overlay functions and routes based on the original IP headers.


# Diffie-Hellman

DH is a public key technology
It is used to securely transfer the shared key over an unsecure network, through PKI

DH groups:
DH 1,2,5 -> no longer secure
DH 14,15,16 -> secure untill 2030
DH 19,20,21 -> with respective key sizes of 256 bits, 384 bits, 521 bits
DH group 24 is the preferred next generation encryption.