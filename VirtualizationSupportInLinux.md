# Linux Namespaces
Kernel feature that allow for further partitioning of resources, so that it appears to the processes within the namespace, that they have their own isolated instance of the global resource. They are a form of lightweight virtualization (containers).
# Which ones are there to use?
1) Mount Namespaces
    - Mount points and file system
2) PID Namespaces
    - Processes
3) IPC Namespaces
    - Inter-process communications
4) cGroups Namespaces
    - CPU, Memory, Output (Control Group)
5) UTS Namespaces
    - Mostly hostname
6) User Namespaces
    - User
7) Network Namespaces
    - Networking resources
# What is their aim and applicability?
In the case of Network Namespaces we create a separate view of out network interfaces. It basically create an "isolated" instance of the network resources.

# Examples For Network Namespaces
Create Network spaces, devices, links

# What is a veth pair ?
Veth is a virtual networking device. It can act as a tunnel between 2 network spaces.
# What is a virtual switch ?
Virtual equivalent to a switch.

# Compare Linux Virtual Switch and oVSwitch
oVSwitch supports additional features and protocol stacks like Openflow and Netflow.

# How can you use all this to build network setups?
vlans, veth, bridges etc

# Mininet?
lighweight os virtualization, you can define network and number of hosts. Is implemented using everything discussed above. using mn you can run any linux command on any host, get links up and down for exmaple. You can also customize network parametes such as delay and bandwidth.
