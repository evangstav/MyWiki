# What is NFV?
 NFV involves the implementation of network functions in software that can run on industry standard server hardware, and that canbe moved to, or instantiated in various locations in the network.

 # Network Function(NF)
A functional building block within a network infrastructure, which has well defined external interfaces and welldefined functional behaviour. Usually it is built around specific HW. Examples are Firewalls, Loadbalancers, switches...

## Network Service
The sum of muliple network functions working together in a system. Service Chaining.

## Network Slice
A network slice is a set of Network services. It is possible to split the network service offer of a Cloud Provider in a set of network slices:
- per tenant
- per industry
- combined

## NaaS
A slice over the provider's architecture to cover the needs of a specific tenant or application.


# What is a vNF?
vNF is a NF but implemented in software, decoupled from specific hardware.
Utilizing vNFs instead of traditional NFs, we can:
- Maximize HW reuse.
- Minimize electric consumption
- Increase flexibility and scalability

# Why is this interesting?
1) Reduced CAPEX & OPEX
2) Redundancy: infrastructure level + vNF level
3) Modularity: Functions as sets of Modules: Microservices mode(Cloud Native design)
4) Elasticity & Scalability
# For who?
# What is SDN and how is it realted to NFV?
SDN allows for controliling the forwarding plane, by decouppling control information and decisions from network elements. By centralizing this control in a single entity, network behaviour can be controlled programatically.
With the help of SDN service chaining can be changed dynamically and on demand.

# Examples of NFV-based Telco services?
1. Virtualizing Customer Premises Equipment
2. Virtualizing LTE's Evolved Packet Core
3. Virtualizing RAN (C-RAN)

# What is ETSI NFV Framework
ETSI-NFV framework is an architectural framework, for NFV standarization.
Its basic requirements are:
- Decoupling HW and SW
- Automated and Scalable Deployment of NFs
- Network state control and monitoring at different granular levels.
# What are its components
1. Operation & Billing Support System (OBSS): collections of systems/interfaces/applications that a service provider uses to operate its business
2. Virtual Network Funcitons (VNFs):
    1. Element Managers(EM): responsible for FCAPS management of the actual network application residing in the VNF (only the functional Part)
    2. Virtual Network Fuctions(vNFs)
3. Network Function Virtualization Infrastructure (NFVI):
    1. vCompute, vStorage, vNetwork
    2. Virtualization layer
    3. computing, storage, network HW
4. NFV Management and Orchestration(MANO):
    1. NFV orchstrator:
        * Resource Orchestration: Allocation and management of NFVI resources to VNFs
        * Service Orchstration: Managing VNFs, their service chaining and the service requirement (KPIs).
        * Keeps e2e view of infrastructure(network) and services
    2. VNF Manager:
        * VNF Life Cycle Management
        * FCAPS(fault, configuration, accounting, performance, security) management of the virtual infrastructure supporting the VNF.
    3. Virtual Infrastracture Manager (VIM):
        * Maintain HW Repository
        * Tracking HW state and utilization
        * Interacting and Managing the Virtualization Manager(Hypervisor):
            * Tracking allocation of HW resource to virtualization pool.
        * Interaction with other MANO elements to enable VNF connectivity through the NFVI.

## Operational Example
1. New Service is requested
2. NFVO has e2e view of the existing and the needed topology
3. NFVO request the VNFM for the required VNFs
4. VNFM determines the necessary resources needed and communicates the requirement to the NFVO
5. NFVO check for resource availability
6. NFVO request VIM for instatiation of the supporting infrastructure (Vms, nts)
7. VIM ask the virtualization layer to create those
8. Upon creating hypervisor inform VIM
9. VIM reports to NFVO about infrastructure availability
10. NFVO informs VNFM of resource allocation.
11. VFNM configures VNFs.(EMs)
12. VNFM inform the NFVO that the VNFs are available to use.
