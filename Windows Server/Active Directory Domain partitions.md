#ActiveDirectory 
### With the active directory forest structure you can manage your domains to solve:
- organisational needs
- to solve problems with replication.
	- if you have a remote site you can give that site a separate subdomain , this way you dont need to replicate 


## The domain partition contains ADUC
this partition is replicated across all DCs inside a DOMAIN
## The configuration partition contains Sites and services
this partition is replicated across all domain controllers in the forest
also MSexchange properties
## The schema partition contains all the templates of the AD objects
is replicated across the complete forest.

For example inside the schema is a template of how a user account looks like, properties, attribures....

## The application partition contains The DNS zone files
is replicated across the full forest.

When you make your dns active directory aware, AD will take care of the replication of the zone files across the dns server (domain controllers)