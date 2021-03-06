# Lecture 2: Datacenter Networking

## Datacenter Network Architecture:
### 1) Traffic Distribution
### 2) Basic 3-tier Network Architecture:
    1) LAG
### 3) Fat Tree: Cheaper
    1) ECMP
    2) Clos Network/Folded Clos Network
    3) Time and Space Switching
### 4) Butterfly Network:
    1) Benes network
    2) Banyan Network (Half Benes) / Butterly Network
### 5) Flattend Butterfly:
    1) More ports 
    2) Less Nodes -> Lower Latency
    3) Bandwidth Limitations

## Interfaces:
### 1) Ethernet Evolution::
    1) Frame Structure
### 2) Vlan::
    1) port-based VLAN::
        1) Split a switch in parts.
        2) Span multiple switches:
            1) trunk port -> additional header in ether 802.1 -> 802.1q
        3) 12 bits
    2) Q in Q MAC in MAC
### 3) MPLS::
    1) Separate forwarding and Routing (forwarding table) Slow??
    3) FEC
    4) Shim header 24 bits 
    5) Label Stacking
    6) Core LSR:
        1) Label Switching
    7) Edge LSR:
        1) Inserting/Popping
    8) Pave the way for mpls
### 4) VxLan::
    1) VxLAN Overlay:: Layer 2 *overlay on top of layer 3*
    2) VxLAN Network identifier 24-bit
    3) Only hosts with same Virtual Network Identification are allowed to communicate
    4) VxLAN Tunnel End Point (VTEP)
    5) VxLAN gateway:
        1) layer 2
        2) layer 3
    6) VxLAN MAC learning

[|Exercises](CloudNetworkingLeture2Ex.md)
