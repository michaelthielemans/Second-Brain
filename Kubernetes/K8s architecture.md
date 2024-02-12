#kubernetes 

# Networking
## Cilium
- Cilium is a eBPF based networking solution for kubernetes, it does layer 3 and layer 4 networking, routing , observability and security and a little layer 7
- the configuration of cilium is done in the resources managed in the control plane.
- Each node has a cilium agent running, the agents will pull the configuration out of the resources you have configured.
- the agents are running as pods on the nodes

currently the reverse proxy feature is handeled by the envoy pod

#### Cilium agents
The agent is installed on a node in the cluster and only handles specific network tasks of that node

#### Cilium operator
The operator handles all the tasks that can not be handled by the agents
Like garbage collection, cleaning the leftovers when a node is removed from the cluster
Handles Cluster global tasks
#### Cilium CLI
Let you control the cluster, get global status of the cluster
you can use this CLI to install cilium onto a k8s cluster
### Envoy
layer 7 routing, policies and security. envoy consumes more resources than the cilium layer3,4 

## Hubble observability and monitoring

it receives metrics from cilium and envoy

#### hubble relay
is the component that receives all the metrics from the different cilium agents and envoy resources.

Hubble has a UI but also a CLI to check the metrics and view dashboards