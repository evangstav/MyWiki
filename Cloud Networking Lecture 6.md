= Network Function Virtualization = 


## Network Function
A functional building block within a network infrastructure, which has well defined external interfaces and a well defined functional behaviour.
For example firewalls, loadbalancers etc.
## Network Service
The sum of muliple network functions working together in a system. Service Chaining.
## Network Slice
A network slice is a set of Network services. It is possible to split the network service offer of a zCloud Provider in a set of network slices:
- per tenant
- per industry
- combined
## NaaS
A slice over the provider's architecture to cover the needs of a specific tenant or application.


# vNfs
1) Pros
- Modularity
- Elastcity - Scalability
- Faster Design/Testing
- Downtimes minimized
- Location and time based deployments
- life Cycle Management
- Multitenancy
- Automation & Programability
- DevopDevopss

2) Cons
- Latency and Throuput perfomance
- Instantiation/decomision time
- Infrastructure Reliability
- Stability and high availability
- licencing
- security:
    - Increased flexibility
    - Multple points of failure.
- migration and management:
    - Evolution vs Revolution
    - Multiple levels of Management
- Resources dependency:
    - Infrastructure sharing & "noisy neighbour effect"
- Troubleshooting:
    - Multiple debugging levels
- Standarization:
    - Evolving....(containers)
    - Impact on interoperability

## Service Chaining

## Netwrok Function Virtualization
- Decouping Software and hardware
- Automated and scalable deployment of NFs
- Netwrok-state control and monitoring at different granular level

## ETSI-standarization for NFV
=== NFV Management & Orchestration (MANO):: === 
Lifecycle management of the physical and virtual resources that comprise the NFV environment.
- NFV Orchestrator:: Provides network-wide orchstration and management of both VNFs and NFVI. (Openstack)
- VNF Managers:: Provides lifecycle management for the VNF.
- Virtual Infrastructure Managers:: Provides resource allocation notifications for resource management and is responsible for CRUD( Create Read Update Delete) operations on the VM level, including creating and destroying connections between the VMs. It will also track configurations, image and usage information. Its interface to the NFVI is where the mapping of physical and virtual resources occurs. Particularly in the area of network provisioning, especially where complex topologies are involved, this is often associated with the SDN controller.
### NFVI
Virtualized compute, storage and network and its corresponding physical resources. The execution environment for the VNFs.
### VNF domain
The virtualized network functions and their management interfaces.


[|Ex6](CloudNetworkingEx6.md)
