# Host Virtualization

1) How do we define "Host Virtualization" in the context of computer envronments 
2) What is a virtual machine?
3) What is an hypervisor, in a virtualization context?
4) Are there diffrent types?
5) How do hypervisors enable netorking of virtual machines? Networking Modes, Types?

[|Ex5](CloudNetworkingEx5.md)


## Virtual Box Network Types
NAT:: NAT means that the virtual machines will have private IP addresses that are no routable from outside.

Bridged Adpter:: Bridged adapter means that any virtual machine running will try to obtain an IP address from the same source your currently active network address got its IP adress.
So the virtual machine shares the same network as the host machine. For all practical purposes the virtual machine is another machine on your LAN.


