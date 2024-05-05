## Adding modules inside a environment

```
environment/
	modules/
		module_name/
			init.pp
			hallo.pp
```


Inside the init.pp you add classes
```
class helloworld {

    notify { 'hello, world!': } #this is a resource

 }
```

# Manually pulling the configuration from the master to the agent node

- Login on the client machine
- Start the pull request with:

```
sudo /opt/puppetlabs/bin/puppet agent –test
```