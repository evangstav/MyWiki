# Lecture 3
# Fundamentals

## Linux/Netoork Namespaces
Namesspaces:: 
- Kernel feature that allow for further partitioning of resources
- Filesystems Namespaces
- PID Namespaces
- IPC Namespaces
- Cgroups
- UTS -> *hostnames*
- User Namespaces


## Veth Space
Virtual Ethernet link

== Namespace to Namespace == 
We will emulate two hosts connected via ethernet by Namespaces and Virtual Ethernet within our virtual machine.

** Create Namespace*
- sudo ip netns add nsH1
** activate local interface*
sudo ip netns exec nsH1 ip link set dev lo up
** create ethernet link with veth and connect one side to NS1*
- sudo ip netns exec nsH1 ip link set veth1 type veth peer name veth2
** connect second side to NS2*
- sudo ip netns exec nsH1 ip link set veth2 netns nsH2 
* add ip address to the veth interface for each device
- sudo ip netns exec nsHi ip addr add <ip-address-i> dev vethi

## Switch Connectivity

Emulate a network based on the same 2 hosts and a switch.
We will create an additional namespace for the switch (Bridge) and link the hosts to it.

## IP masquerade
IP Masquerade is the linux function that allows a set of machines to *invisibly * access the Internet via the MASQ gateway even *without an official ip address. To the other machines on the internet, the outgoing traffic will appear to be from the IP MASQ Linux server itself.

## IPtables
!!TODO
[/](https://iximiuz.com/en/posts/laymans-iptables-101.md)
[s](https://opensource.com/article/18/10/iptables-tips-and-trick.md)
Firewall utility..

## Virtual Switches

## Mininet




[|Ex3](CloudNetworkingEx3.md)
