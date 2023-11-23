## admin distance

0 =  directly connected
1 =  static routes

## Routing types

- standard static route
- default static route
- floating static route 
	- -> is a route with an higher AD
- summary static route

### static route hop options

- next hop route `ip route x.x.x.x <net-mask> <nexthop route>`
- directly connected static route ` ip route x.x.x.x <net-mask> <interface-ID>`
- fully specified static route `ip route x.x.x.x <net-mask> <nexthop route> <interface-ID>`
- static hosts route: `ip route x.x.x.x /32 <nexthop route>`