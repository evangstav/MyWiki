# Datacenter Networking

## Traffic Distribution in Datacenters
The bulk of traffic we need to manage in a datacenter comes from communication within the datacenter. A Cisco example mentions that 77% of the traffic is within the Datacenter, 14% Datacenter to user and 9 percent Datacenter to Datacenter. So like 3/4 of the traffic is internal. So most of the data traffic is _East-West_ compared to _North-South_

## Datacenter Architectures

### Basic 3-Tier Architecture
            Core-Switches
               /  \
              /    \
      Agg.Switch  Agg.Switch 
         /\           /\   
        /  \         /  \
       /    \       /    \ 
      TORs  TORs   TORs  TORs
      Svs   Svs    Svs   Svs
      
In the basic 3-Tier Architecture, servers are placed in racks, with one or teo Top Of the Rack Switches (TORs). The interconnection between the TORs is established using several bigger aggregation switches often connected via SHort Reach (SR) optics. These swictches are in turn interconnected through few massive Core swiches, using Long Reach (LR) optics.

This is expensive since large switches are costly to buy and maintain.

### Clos and Fat-Tree
Fat-Tree architecure is Based on Clos Network and incorporates many relatively small switches throughout the network. Specifically there are k pods, each containing k switches. Each switch has k ports, and a network build out of k switches has k^3/4 hosts.
The main advantage of this design is that all switching components are identical and relatively small. Although the number of switches in a fat tree network would be bigger than in a 3-Tier the cost will be much lower, since large switches are more expensive than the equivalent number of small switches.Also it is more scalable for the same reasons. You can always get more switches but building larger switches becomes harder and more inefficient.

### Underlying Design Principles
1) Scalability
2) Energy Efficiency
3) Cost

## Purpose of overlay/virtual Networks in DC
Physical Network resources are divided up among multiple virtual networks. They enable multitenancy. That way each tenant as its own virtual network, isolated from the other tenants of the datacenter.
Also connections between datacenters for same tenants.


### Virtual Networking Technologies

1) Vlan
    - Port based VLANs -> One virtual operates as multiple switches.
    - VLANs can be spanning multiple switches via a "trunk" port.   
      * Frames forwarded via trunk port can't be regural ethernet frames -> vlan headers -> 802.1q protocol
2) Q-in-Q
    - 5 bit tag after ethernet header(between ethernet header and payload)

4) MPLS
    1) Separate forwarding and Routing (forwarding table) Slow??
    3) FEC
    4) Shim header 24 bits 
    5) Label Stacking
    6) Core LSR:
        1) Label Switching
    7) Edge LSR:
        1) Inserting/Popping

5) VXLAN
   1) VxLAN Overlay:: Layer 2 *overlay on top of layer 3*
   2) VxLAN Network identifier 24-bit
   3) Only hosts with same Virtual Network Identification are allowed to communicate
   4) VxLAN Tunnel End Point (VTEP)
   5) VxLAN gateway:
       1) layer 2
       2) layer 3
   6) VxLAN MAC learning



  
