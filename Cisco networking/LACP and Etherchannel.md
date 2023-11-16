#cisco #networking #switching 

LACP = Link Aggregation Control Protocol = IEEE802.3ad -> IEEE802.1AX
PagP = Port Aggregation Protocol = cisco proprietary 

## LACP states

> on : forced on and no negotiation
> Active : initiates negotiation
> Passive : only respond to lacp negotiation packets

## PagP states

> on : forced on and does not send negotiation packets
> PagP desirable : initiates negotiation with counterpart
> PagP auto : passive negotiation state, only responds to PagP packets

## LACP configuration

`(conf)# interface range fa0/1-4`
`(conf)# channel-group 1 mode <active-passive-on-desirable-auto>`
## show commands

> `#show interface port-channel 1`
> `#show etherchannel summary`
> `#show etherchannel port-channel`
> `#show interface fa0/1 etherchannel`
> 