# [Kubernetes](Kubernetes)
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
The scheduler in the case of Kubernets decides POD alocation on nodes, and updates the POD definitions in APIsrvr.
The scheduler operation is a 2-step process:
1. Filter the list of nodes to find the subset of nodes the POD can be scheduled to.
2. Choose the best node according to some prioritization policy. If multiple nodes are equally good -> round robin -> even distribution
## What is Kubernetes?
The de facto standart container orchestratoe developed and opensourced by google together with linux foundation. Muti-container tech (not nly docker)
### Terminology
- Pods : Deployable unit of functionality = One or more containers, collocated in a host and can share resources.
- Services: Set of Pods working together:
    - Service Discovery based on Kubernets DNS

## What are its components
- Master Node -> Control Plane -> Cluster managemet traffic
- Worker Nodes -> Data Plane -> Application Traffic

### Control Plane Componenents
1. etcd
2. API Server
3. Scheduler
4. Controller Manager

### Worker Node Components
1. Kubelet
2. Kubernetes Service Proxy
3. Container Runtime (docker)

### Add-ons
1. Kubernetes DNS server
2. Dashboard
3. An Ingress Contoller
4. Heapster??
5. Container Network Interface (CNI)

## What is Container Network Interface (CNI)?
CNI is a minimal specification to be a simple contract between the container runtime ans the network plugins. A JSON schema defines the expected input and output from CNI network plugins.
It provides a GO implemented API between runtime and Network Plugins.

## What are the networking modes for Docker containers used in Kubernetes?
https://itnext.io/an-illustrated-guide-to-kubernetes-networking-part-1-d1ede3322727 (nice illustrative link)
_Every Pod has a unique IP._
### Intra Node Networking
PODs in the same node belong to the same ip subnet. Each POD has a veth interface connected to a (Common) bridge interface in the node. That away all Pods in a node have connection to each other.
### Inter Node Networking
Solutions based on overlay/underlay or simple routing. In case of 2 nodes routing tables in Node1 must be configures so that packets to Node2 POD subnet are routed to Node2 and vice versa.

## Service Discovry
- Based on EVs
- Based on DNS

## How are Services exposed in Kubernetes?
Services are a single constant point of entry to a group of PODs providing the same application.
- Identified by a single constant tuple (IP@, port)
- Kubernets will route the request to one of the PODs defined in the service.

!NOTE we can't ping this ip@ since it does not correspond to a real machine.

There are 3 mechanisms in Kubernetes to expose a Service:
1. Service type as NodePort: the nodes open a dedicated port and redirect traffic arriving on that port towards the realted service
2. LoadBalancer: extension of NodePort; Kubernetes creates a LB which receives the requests to its IP@ and forwards to the corresponding NOdePorts for the service Nodes.
3. Ingress resource: HTTP level mechanism that allows to expose multiple Services through a single IP@.
### Implementation
Everythin related to services is handled by the kube-proxy process running on each Node.
- When API Srvr creates a service, the kube-proxy in each node enables IP-tables so that packets to (ServiceIP@:port) are modified (destination@:port) and send to a pod backing the Service.
- kube-proxy watches for changes in API srvr and in Endpoints (lists of PODs backing services)
