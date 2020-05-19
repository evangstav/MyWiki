# DockerSwarm
## What is the cattle approach for managing containers?
In the cattle approach machines are treated anonymously.
- They are all identical
- Applications are automatically deployed in any of the machines.
- Automatic redployment in case of failure

## Which Functions need to be provided by a container orchestrator?
- Allocations of Applications into Nodes(Scheduling)
- Service Discovery (Redirecting requests to the right node)
- Health Checking (node vs Service vs Service Components)
- Upgrading(Distributed system ,OS, apps)
- Scaling
## Which Functionality does the scheduler provide in a container orchstrator?
## What is Docker Swarm?
Docker swarm is a container orchestratio tool. Applications required such coordination are termed *Services* in Docker. Service can be further split into *Tasks*(containers), which are allocated to specifi nodes within the cluster of hosts.
## What are its components?
Docker Swarm has 2 types of Nodes:
1. Manager/Master: it is responsible for the configuration of the swarm nodes to provide the services (scheduling)
2. Worker Nodes: they are responsible to execute the tasks assigned by the manager, by running specific containers. When defining a service docker allows to define its desired state. _The manager of the swarm will coordinate the workers to assure this state_.
## What is the networking mode for Docker Containers used in Docker Swarm?
Intra swarm communication: Docker Swarm enforces TLS mutual authentication and encryption among nodes, to secure communications.

When initializing or joining a swarm, 2 networks are created on the host:
1. Ingress: *overlay network* for swarm control and swarm data traffic.
2. docker_gwbridge: connects the Docker daemon in the host to the other daemons in the swarm.
## How are services exposed in Docker Swarm?
- To expose services outside the Swarm, Docker uses *ingress load balancing*. For each service, Docker Swarm provides a published Port on any node in the cluster.
- Each Service get assigned an internal DNS entry. This is used by the manager for internal load balancing of requests.
- Routing Mesh: DockerSwarm redirects the request for a published port to a worker, transparentl. *There is no guarantee about which node will be serving the request.
 
!!Note Ingress network is not a bridged net but an overlay(virtual) one.
It is good practice to create swarm service in separate overlay networks.
