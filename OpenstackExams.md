# [Openstack](Openstack.md)

## What is Openstack?
Open Source data center resource management software. It provides a common platform to manage clouds of servers, storage, networks and even application resources.
OpenStack can be understood as a software platform that uses pooled virtual resources to build and manage clouds, both public and private ones.
## Which fucntionality does it fit in the ETSI NFV archtecture?
VIM
## How does it fit in the cloud models?
It can be seen as an IaaS model.

## What are Openstack components?

1. Horizon: Dashboard functionality, gui for the whole system
2. Keystone: Role Based Access Control (RBAC) to services and infrastructure, user authentication
3. Glance: VM-types(Image) repository and metadata, discover, register and restore images
4. Swift: Object-storage(VM-images etc.), convert to objects and stores in DB
5. NOVA: used to manage compute resource in a scalable way.
6. NEUTRON: enables and manages connectivity among compute-instances and the outside world.
7. CINDER: Block storage
8. HEAT: Template-based orchestration service
9. CEILOMETER: Monitoring and telemetry service

## Which types of network does Openstack support?
1. By Ownership:
    - Project or Tenant Nt: Virtual network created by a project or an administrator on behalf of a project, to *provide connectivity to resources within a project*.
    - Provider Nt: virtual network created by an admnistrator, to map a physical network. Typically to enable access to *resources outside the cloud*.
2. By function:
    - External Networks: They represent a view into a slice of the physical external network, accesible outside Openstack installation (public).
    - Internal Networks: They connect directly to the VMs. Provide direct connectivity (L2) to the VMs attached to them (private).
        * To connet different internal networks, routers (L3) are necessary.
        * To conect an internal network to an external network, a router (L3) is necessary.
3. By Type:
    - Local: isolated from other networks and nodes.
    - Flat: no 802.1q VLAN tagging is used to segregate traffic. Can expand multiple nodes.
    - VLAN: Use of 802.1q VLAN tagging.
    - GRE: Use Generic Routing Encapsulation(GRE) for communication between nodes. The KEY header is used to segregate networks.
    - VXLAN: Uses VXLAN Network Identifier to differentiate traffic among VXLAN networks. The VNI is used as header to encapsulate traffic over UDP, over L3 nets.
    - GENEVE

## How VMs are instantiated?
1. User requests VM instance via HORIZON
2. NOVA API -Idetnity service
3. nova api -> nova db
4. Nova api -> nova scheduler(set up instance)
    1. Nova scheduler -> nova DB finds a suitable host
    2. Nova scheduler -> nova compute(in target node)
    3. Nova compute -> Image service(identigy and load image loacally)
    4. nova compute -> neutron service (request network configuration for new VM IP@, etc)
        1. Neutron(-> identity service)->keep network config in Neutron Plugin(in target node)
    5. noca compute -> Volume service
    6. nova compute -> Hypervisor(target node)
        1. VM is created and configured
5. The VM is visible through horizon

## How are entities (VMs) assigned to networks in Openstack?
1. Nova attaches VM instances to virtual switches on the hosting compute node, via the VM's virtual network interface (VIF).
2. VIF is configured as per Neutron port-info in Nuetron DB
    * Linux Bridge:
        * VIF is connected to the bridge of the associated network
        * Different Bridges for each different L@ network in the compute node.
    * OvSwitch:
        * VIF is plugged into the br-int of the node
        * vswitch port is configured with local VLAN-ID corresponding to the network associated withthe Neutronport and VIF.


## How many switches/bridges can you find in an Openstack network?

## How does Openstack provide network isolation among different customers and entities?
With Linux Bridge network isoaltion within compute node is topology based, while with OvSwitches is VLAN based.

## More on OvS Networking on Openstack:
3 bridges are used for creating network topologies:
1. Intergation Bridge (br-int): central switch in the node connecting the cirtual devices. Sometime( when neutron Security groups and iptables firewall is used ), VMs are not directly connected to it, instead they use individual linux bridges, connected to br-int.
2. Provider Bridge(br-ethX): provides connectivity to the physical network via physical interfaces. Each provider bridge is associated with a physical interface. They are connected to the br-int with a OvS patch cable.
3. Tunnel Bridge (br-tun): it is used to connect GRE and VXLAN tunnel end points. SDN-flow rules are responsible for encpsulating tenant traffic traversing it.

Each controller, network, or compute node is the OS setup has its own br-int and br-ethX bridges.
