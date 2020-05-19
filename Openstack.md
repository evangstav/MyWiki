# Openstack

## What is Openstack
OpenStack is an open source platform, which offers powerful virtual servers and required services for cloud computing. It is mostly deployed as Infrastructure-as-a-service (IaaS), which aims to provide hardware tools and components for processing, storage, and networking resources throughout a data center.
OpenStack can be understood as a software platform that uses pooled virtual resources to build and manage clouds, both public and private ones.

## Openstack Functional Architecture

## Openstack Setups
Usually:
- Controller Node: 1 single entity. Provides Service-servers + DashBoard
- Network Node: 1 single entity. Provides Neutron services agents (DHCP, Metadata, L3, ...)
- Compute Nodes: Multiple entites. Host Neutron plugin agent, nova-compute + Hypervisor (KVM, Hyper-V, Xen) / (LCX/Docker)
- Storage Nodes: Keep image repos


## Openstack Networking
1) Neutron provides Networking services and exposes an API to users(other Openstack services). Network info/vonfig is stored i a DataBase.
2) Neutron agents: implement networking functionality in the nodes (they form client server relations with the neutron server). They communicate with the server via an internal messagin queue.
3) Network topology and configuration persistend in DB.

### Networking Features and Enablers
- Switching: L2 connectivity. Provided by::
    - Linux Bridge
    - ovSwitch
- Firewalling: traffic filtering. Enabled by::
    - Security Groups (IPTables)
    - FWaaS
- Load Balancing: LBaaS OpenStack service

### Network Types in OS
1) By Ownership::
    - Project or Tenant Nt: Virtual network created by a project or an administrator on behalf of a project, to *provide connectivity to resources within a project*.
    - Provider Nt: virtual network created by an admnistrator, to map a physical network. Typically to enable access to *resources outside the cloud*.
2) By function::
    - External Networks: They represent a view into a slice of the physical external network, accesible outside Openstack installation (public). 
    - Internal Networks: They connect directly to the VMs. Provide direct connectivity (L2) to the VMs attached to them (private).
        * To connet different internal networks, routers (L3) are necessary.
        * To conect an internal network toan external network, a router (L3) is necessary.
3) By Type:
    - Local: isolated from other networks and nodes.
    - Flat: no 802.1q VLAN tagging is used to segregate traffic. Can expand multiple nodes.
    - VLAN
    - GRE
    - VXLAN
    - GENEVE

### Neutron Terminology
1) Network: Isolated L2 broadcast domain.
2) Subnetwork: Address block from which IP addresses can be allocated to VM instances. *MUST* be associated to a network.
3) Port: Logical representation of a Virtual Switch port. VM interfaces are mapped to Neutron ports, which define the MAC and IP address to be assigned to the interfaces plugged into them. Their definition is stored in Neutron's DB and it is used by Neutron agents to buikd and connect the virtual switching infrastructure.

### Network Isolation mechanisms is OS: multitenancy -> isolated networks
1) Network Namespaces: logical copy of nt. stack with own routes, FW rules, and nt. Interfaces.
    * Isolated DHCP and routing services per network.
    * Allows to have overlapping setups and configurations (IP @s) accros projects.
    * Naming Convention:
        - DHCP namespace: qdhcp-<nt UUID>
        - Router namespace: qrouter-<router UUID>
        - Load-Balancer namespace: qlbas-<lb UUID>

### Creating Instances and Networks: Linux Bridge vs OVs
- With Linux Bridge network isolation is topology-based(different bridges for different neworks).
- With OvS network isolation within the compute node is VLAN based(The tagging is visible only to the switch. The VMs are not aware of it).

#### Attaching Instances to Networks
Nova attaches VMs to virtual switches, on the hosting compute node, via the VMs virtual network interface (VIF). Then the VIF is configured as per Neutron port -> info in Neutron's DB.
- If the network is based on LinuxB:
    - The VIF is connected to the bridge of the associated network. Different bridges for each different network at L2 in the compute node.
- If the network is based on OvS:
    - The VIF is plugged into the intergration-bridge of the node. The vswitchh port is configured with a local VLAN-ID, corresponding to the network associated with the Neutron port and VIF.

#### Linux Bridge in Openstack
- The LinuxB mechanism driver in OS supports Local, Flat, VLAN and VXLAN.
- Flexible and easy to troubleshoot, but does not support advanced features (i.e. SDN).

- Interfaces that can appear in a Linux-bridge OS network:
    * Physical: interface in the host, pluggedd into physical nt HW.
    * TAP: created by the hypervisor to connect the VM to the bridge in the host. It is a virtual interface in the host that corresponds to te VIF in the VM instance. An Ethernet frame sent to the TAP device on the host is received be the guest OS and vice versa.
    * VLAN 802.1q
    * VxLAN
    * Linux Bridge.
- In a LinuxB setup in OpenStack, every nt. uses its own bridge.
- When configured as a trunk port, the provider netowrk Interface( Physical ) in the node can support multiple VLAN nts.

1) LinuxB Network Types: 
    a) Local Network: no external connectivity. Only tap interfacsare attached to the bridge.
    b) Flat Network: The node's physical interface must by connected to the bridge. If there are  multiple networks on the same node, each must be associated with a different physical interface. *Not scalable !*
    c) VLAN Network: When configured as _subinterfaces_, the provider nt. Interface (physical) in the node can support multiple VLAN nts.
    d) VXLAN Network: Based on linux vxlan interfaces, connected to the bridges.
    - !!NOTE on overlay networks: stacking headers can make the packet MTU exceed 1500B !
        * MTUs in VMs VIFs can be lowered (f.ex to 1450 B)
        * MTUs for the interfaces used for overlays (VLAN, VXLAN) and switc ports can be increased to a big value (3000B, 6000B etc.).

#### OvS in Openstack
- The OvS mechanism in OS supports Local, Flat, VLAN, VxLAN and GRE networks.
- Virtual Nt switches and flow rules (SDN) to forward traffic.
- Devices that can appera in OvS OS network:
    * TAP: created by the hypervisor to connect the VM to the bridge in the host. It is a virtual interface in the host that corresponds to te VIF in the VM instance. An Ethernet frame sent to the TAP device on the host is received be the guest OS and vice versa.
    * Linux-Bridge
    * Virtual Ethernet cables: mimic patch cables. An ethernet packet sent to an end is received byt the other end. Used by neutron when connecting nt-namespaces and Linux Bridges or Linux Bridges to OvS bridges.
    * OvS bridges
    * OvS patch cables: specfic veth cables to connect OvSs only.
- OS uses 3 specific OvS "bridges" for creating topologies in and between computer Nodes::
    * Integration Bridge (br-int); central switch in the node, connecting most of the virtual devices. Sometimes( when Neutron Security Groups enabled and the iptables firewall driver is used ), VMs are not directly connected to it. Insted there are individual linux brides per instance, connected to the int-br.
    * Provider Bridge (br-ethX): provides connectivity to the physical network via physical interfaces. Each provider bridge is associated with a physical interface. They are connected to the br-int with an OvS patch cable. 
    * NOTE: Each controller, network or compute nodes in th OS setup has itsown br-int and br-eth bridges.
    * Tunnel Bridge (br-tun): it is used to connect GRE and VxLAN tunnel endpoints. SDN-based flow rules are responsible for encapsulating tenant traffic traversing it.

1) OvS Netowrk types:
    a) Local Network: no external connectivity. Only br-int. 
    b) Flat Network: br-int and br-ethX. Flat networks are treated VLAN networks.
    c) Overlay networks: VxLAN and GRE. Tunnel Bridges (br-tun) in tunnel endpoints.

#### Dynamic IP@ allocation
- Neutron DHCP agent:
    - In Controller or dedicated Network nodes.
    - Responsible fro creating a local network namespace that corresponds to each network scheduled to that agend.
        * A DHCP server per network.
        * A DHCP server nt namespace: qdhcp-<nt UUID>
    - An IP@ configured on a VIF inside the namespace (server!), together with a dnsmasq process listening for DHCP requests on the nt.
        * DHCP request-based mechanism: a client is allocated an IP@, dynamically, at start-up.


## Connecting Networks
- Reason: Interconnecting user-created nts, as well as with extenral nts.
- Neutron L3 agent provides routing and NAT services to  VM istances within the cloud. It uses Nt namespaces to provide isolated routing instances.
- Current versions of OpenStack: Stand alone routers, termed "legacy routers" vs new proposals based on distributed virtual routers.
- A router in OpenStack is usually connected to a single external provider nt and 1 or more project networks (NAT). 
- Routing tables within the namespace dictate how traffic is routed, and iptables-rules dictate how traffic is translated (NAT), if necessary.
# Distributed Virtual Routers
- Only supported by OvS driver & agents.
- Neutron distributes a VR across compute nodes, so that no particular node constitues a point of failluer.
    * Routing is not carried out by the L3 agent in the Network Node but in the Compute-nodes.
    * VMs are unaware of the location of the router (seen as single entity).

