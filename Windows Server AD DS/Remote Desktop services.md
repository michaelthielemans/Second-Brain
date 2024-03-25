#windows 
- (old name is terminal services)
- Cloud variant : Azure virtual desktop

.rdp shortcut. hierin staan alle settings om een bepaald applicatie remote te draaien.


## Terminal services in windows server
- Terminal server
- Terminal services Licensing
- Terminal services session broker
- Terminal services Gateway
- Terminal services Web Access

#### The Terminal Server role service
Enables a server to host Windows-based programs or the full Windows desktop.
#### Terminal Services Licensing
Manages the Terminal Services client access licenses (TS CALs) that are required to connect to a terminal server. You use TS Licensing to install, issue, and track the availability of TS CALs.
#### Terminal Services Session Broker
Enables a user to reconnect to the server which contains their existing session in a load-balanced terminal server farm. If a user disconnects from a session (whether intentionally or because of a network failure), their applications will continue to run. When they reconnect, TS Session Directory is queried to determine whether they have an existing session, and if so, on which server in the farm. If there is an existing session, TS Session Directory redirects the client to the terminal server where their session exists. This functionality prevents the user from starting a new session if the user already has a disconnected session. The TS Session Broker performs load balancing even if a load balancer is not in place. It is designed to allow for “session draining” to phase out sessions from the server when taking the server offline for maintenance.
#### Terminal Services Gateway
Helps provide secure remote connectivity to terminal servers and remote desktops on the corporate network, from anywhere on the Internet..

#### The Terminal Services Web Access feature
Lets users access Remote Programs through a Web site.


## TS gateway
Why installing a RDS gateway?
- Allows connections from outside.
- Only the HTTPS port needs to be opened to the outside world -> less ports need to be opened on the internet firewall.
- It does HTTPS off-loading
- inside the https there is a RDS packet


#### TS Gateway Benefits
- Provides a comprehensive security configuration model that enables you to control access to specific resources on the network.

- Reduces management costs by removing the need for application servers at distributed locations.

 - Facilitates consolidation of existing terminal servers using x64 technology.

- Can be integrated with Network Policy Server (NPS), enabling you to centralize the deployment of TS Gateway policies and reduce the total cost of ownership (TCO) for your organization.

- Allows monitoring of status, health and events on remote connections.

- Enables users to connect remotely to terminal servers and remote desktops across firewalls and network address translators (NATs).

- Eliminates the need to configure VPN connections to enable remote users to connect to the corporate network through the internet.  You can place the Windows Server 2008 terminal server behind multiple firewalls without opening multiple firewall ports other than 443.

##### You should use TS Gateway in place of a VPN in the following circumstances:

- When no local copy of data is required.
- When a quicker connection time is required.
- When bandwidth or application data sizes make a VPN experience less than optimal.


## RemoteApps

When a client connects to a server running Windows Server 2008 Terminal Services RemoteApp, a number of changes are implemented:

- Instead of being presented to the user in the desktop of the remote terminal server, the remote program is integrated with the client's desktop, running in its own resizable window with its own entry in the taskbar.
- If the program uses a notification area icon, this icon appears in the client's notification area.
- Popup windows are redirected to the local desktop.
- Local drives and printers can be redirected to appear in the remote program.

###### An administrator must perform the following steps to configure a TS RemoteApp Server:

- Enable Remote Connections
- Add the TS RemoteApp Snap-In
- Configure TS RemoteApp
- Install applications on to the server running the Terminal Server role service
- Run the RemoteApp Wizard to add a program to the Allow List and make it available remotely to users
- Create an RDP Package or an MSI Package to use for deployment
- Distribute RemoteApp programs to Users.  You can distribute the .msi file to the end user’s local computer by using your normal distribution process, such as Microsoft System Management Server or Active Directory group policies.

##### Users can run RemoteApp programs in a number of ways:

- Double-clicking an .rdp file that has been created and distributed by their administrator. (Administrators can distribute an .msi file to create shortcuts to .rdp files on users' desktops or in the Start menu.)
- Double-clicking a file whose extension is associated with a RemoteApp. This can be configured by their administrator using an .msi file.
- Accessing a link to the program on a Web site using Terminal Services Web Access.