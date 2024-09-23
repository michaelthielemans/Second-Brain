Written in ruby
### Puppet uses:
- declarative language for expressing system configuration
	Tel how to system config should like like
	NOT how or what has to be changed.

### key components in puppet
- puppet client  => client agent on the target client machine, puppet agent software installed
- puppet master => server , responsible for maintaining the configuration

### Communication between client and master
SSL communication between master en agent
-> need for certificates
-> ip address, hostname, certificate name moet correct zijn.


### How puppet works
1. Agent stuurt periodiek FACTS naar de puppet master.
2. The puppet Master uses this data and compiles a list with the configuration to be applied to the agent. This list of configuration to be performed on an agent is known as a catalog. This could be a package installation, upgrades or removals, a file system creation, a user creation or deletion, a server reboot, IP configuration changes, etc.
3. Master stuurt CATALOG naar puppet-client
4. The agent applies the settings that are defined in the catalog he has received.
5. The agents reports back to the master, the report indicates what happened on the client


![[Pasted image 20240612194412.png]]