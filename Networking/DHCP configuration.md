#cisco 

1. add exclude addresses
	`(conf)# ip dhcp exclude-address x.x.x.x`
2. define pool and name
	`(conf)#ip dhcp pool "name"`
3. configure the pool
```
(dhcp-conf)#network x.x.x.x
(dhcp-conf)#default-router x.x.x.x
(dhcp-conf)#dns-server x.x.x.x
```	