# add the repository
```
wget https://apt.puppetlabs.com/puppet6-release-focal.deb
sudo dpkg -i puppet6-release-focal.deb
```

## Install the package

```
Sudo apt-get update -y  
sudo apt-get install puppet-agent -y
```

## Adjust the puppet-client configuration
```
vim /etc/puppetlabs/puppet/puppet.conf
```

***Puppet uses four configuration sections in its puppet.conf file:

- **Main:**
	is the global section used by all commands and services. It can be overridden by the other sections.
- **Master:**
	is used by the primary Puppet server service and the Puppet Server ca command.
- **Agent**
	is used by the Puppet agent service.
- **User:**
	is used by the Puppet apply command_

The main section will apply to all run modes, but agent will only apply to the given run mode.

Each configuration setting in puppet.conf also has a corresponding setting on the command line. Options are resolved in the following order, from highest priority to lowest:

**Command line > agent mode > main mode > puppet defaults**

This means that a setting in agent will override a setting in main when running puppet agent -t, but that an option specified on the command line overrides both.






**server** — **The master server to request configurations from**. **Default value is puppet**. Change it if that’s not your server’s name.

**certname** — The node or agent’s certificate name or **HOSTNAME**, and **the unique identifier or hostname it uses when requesting catalogs**. Default value is the fully qualified domain name. For best compatibility, limit the value of certname to only use letters, numbers, periods, underscores, and dashes. That is, it matches /\A[a-z0-9._-]+\Z/.

**environment** — **The environment to request when contacting the master**. It’s only a request, though; the master’s  ENC can override this if it chooses.  
An environment is **an isolated group of agent nodes** that a puppet server can serve with its own main manifest and set of modules. For example, you can use environments to set up scratch nodes for testing before rolling out changes to production, or to divide a site by types of hardware.  
**Default value is production.**

When you run puppet from the command line, how does it know what master to talk to?  
By default, puppet will look for a puppetmaster simply called 'puppet'.  
If the puppet.conf doesn't specify the server to talk to, the agent will use the systems resolver to look for just 'puppet', and if it's able to resolve that name, it will use the returned IP.



**Very important (!): As certname define the hostname of your puppet agent in this case “puppetclient”; otherwise a catalog for the defaultnode will be applied for your puppet agent!**


# Start and Enable puppet on the agent
```
sudo systemctl start puppet  
sudo systemctl enable puppet
```


## Sign Puppet Agent Node Certificate

Type the below command on Master node.

```
sudo /opt/puppetlabs/bin/puppetserver ca list
```

you can see that the certificate ‘puppetclient’ is received.

To sign a certificate, you can execute the cert s

```
sudo /opt/puppetlabs/bin/puppetserver ca sign <name certificate>
Sign all certificates by executing the following command:
Sudo /opt/puppetlabs/bin/puppetserver ca sign --all
```


To list all requests (signed or not signed), we need to execute the following command on the master.

```
$ sudo /opt/puppetlabs/bin/puppetserver ca list --all
```

Verify the communication by typing:
```
Sudo /opt/puppetlabs/bin/puppet agent –-test
```



## Creating the correct directory structure ON PUPPET MASTER:

As long as the dir structure that corresponds to the environment you have defined on the puppet-client it cannot transfer data to the master.

Create the following directory structure:
#### Dir structure of:  /etc/puppetlabs/code/environments

```
ITF/
	manifests/
		site.pp  #main manifest file with refers to “sub” manifest files in the modules with the statement include
	modules/
		helloworld/ (the module name)
	manifests/
		init.pp (contains the helloworld class – **the init.pp manifest is mandatory for each module**)
		motd.pp (contains a file resource that ensures the creation of the motd)

```


>Any module that is environment-specific should go into `/etc/puppetlabs/environments/<env>/modules

>The main manifest file of the environment goes into:
` /etc/puppetlabs/environments/<env -name>/manifests**
> It is common practice to call this file site.pp



>Any module that is common to all environments should go into
>`/etc/puppetlabs/modules or /usr/share/puppet/modules


Adjust the environment.conf file to define the location of the main manifest file.
/etc/puppetlabs/environment/<env>/manifests?**

Defined in environment.conf

Puppet will check following files:
Defined in environment.conf?
	not present?
		check
	            Defined in puppet.conf?
		            not present?
				check
		                        Default value: ./manifests (relative to the environment directory)

You can add a environment.conf file the the root directory of your environment but it is not really needed