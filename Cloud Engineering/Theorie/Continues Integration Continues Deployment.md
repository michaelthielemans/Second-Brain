- Continues Delivery -> Is has a pipeline where there are human safeguards. new versions are not completely automatically applied to production.
- Continues Deployment -> successful automated pipeline will push directly to production. No human safeguards.

# Network infrastructure for service development

## Load balancers
#### Forwarding mechanisms

- round robin
- persistent session
- least connections
- ip hash -> based on the hash of the ip