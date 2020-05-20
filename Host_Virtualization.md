# How do we define host virtualization?
Technology enabling the simultaneous use of *different operative systems* and its applications on a single physical hardware, while providing the an *abstract/isolated* view of this hardware.
- Abstracts physical hardware resources to applications
- Allows sharing of those resources among applications.
# What is a virtual machine?
Virtual machine is an emulation of a computer system. Virtual Machines are based on
on computer layer architecture as reference model, where OS is abstracting physical hardware resources to applications, by providing them specifi interfaces(Device Drivers). So it is a layered approach where OS serves as a layer on top of the hardware that provisions nad manages the use of the hardware by the application on top of it.
## Reference model
| Application1 | Application2 | Application3 |
| OS(drivers)  | OS           | OS(drives)   |
| Hardware     | Hardware     | Hardware     |


# Virtualization types
1. Full Virtualization:
    - Decouples Hardware and OS functionality. Examples Vbox, KVM/Qemu, VMware
2. Para-virtualization / HW-assisted:
    - Some guest OS actions can be applied diretly to hardware( better perfomance )
    - guest OS needs to be modified to allow for coexistence with VL.
    - Ex. Citrix Xen Server
3. OS level virtualization
    - sinle common OS(Linux), but applications with isolated workspaces and resources
    - Linux containers, Docker
    - No hypervisor involved(lightweight)
# What is a hypervisor?
Hypervisor is usually a software that creates and runs virtual machines. A computer on which a hypervisor runs is called a host machine, while the virtual machines created are called guests.
# Are there different types?
1. Type-1 Native or Bare-Metal:
    - Runs directly on Hosts hardware to control the harware and manage guests
    - Higher perfomance
    - (this is the original mainframe design)
2. Type-2 Hosted Hypervisors:
    - Runs on a conventioinal OS like a regular computer program
    - A guest OS runs as a proccess on the host
    - Hardware independent
    - Lower perfomance than native, since it is competing for resources with other programs
    - Popular for X86 architecture
# How to hypervisors enable Networking?
The Hypervisor allows the guests to share the physical network interface card (NIC) of the Host.
Each guest is assigned one (or multiple) virtual NIC (vNIC)
The hypervisor manages these vNICs and their features mapping traffic to/from them.
An easy way of thinking is of virtual switches within the Hypervisor, with vNICs connected to ports of the switch, also allowing for internal VM communication.

Multiple switched networks, with different characteristics, can coexist within a single host. These are "real" networks with virtual elements.
## The trip of a packet in a Virtual Environment
1. Packet arrives at Host NIC
2. CPU is interrupted
3. Host proccesses it and passes it to the hypervisor
4. Hypervisor proccesses the packet
5. Queued/Switched to VM by the Hypervisor
6. Packet arrives at guest's vNIC
7. Share of guest CPU resources
8. vCPU is interrupted
9. Guest proccesses packet from vNIC

So the usual path of packet processing is :
NIC->Kernel Memory(Driver)->UserSpace(US) memory-> Application
For both hosts and VMs

We can see that there is a lot of processing and cpu interupting involved, (overhead) that leads to a perfmance impact(delay, jitter, effective transmission rate, ...).
## Improving Perfomance
1. Data Plane Development Kit (DPDK):
    - Allows access to US memory directly from NIC
    - Much Faster due to increased efficiency
    - Intel Specific
    - Ring buffer is used for transferring packets between the physical NIC and the application using DPDK.
    - Instead of CPU interruptions, a periodic packet poll mechanism is used.
    - Scalar packer processing (stream of sequential packets)

2. Single-root i/o virtualization (SR-IOV)
- The host's NIC takes care of interruptions, making the host CPU unaware of them (it is not interrupted!).
- The NIC itself creates virtual interfaces and presents the to entities above (OS, hypervisor, ...)
    * These virtual interfaces are termed virtual function (VFs)
    * The hypervisor can use these vNICs as physical interfaces to the VMs, connecting them as "pass through".
    * The PCI bus is used for packet exchange between the VFs and the Host.( This may create bottlenecks)
- Needs support from both the HW and the hypervisor(pass-through).

*So both SR-IOV and DPDK avoid Kernel participation in packet handling leading to faster paths.

*SR-IOV vs DPDK*:
    - Nort South Traffic (from vm to outside):
        * SR-IOV(hypervisor not involved in trasmission): Hops from NIC to vNIC and back to NIC. (better)
        * DPDK in Hypervisor's switch: Hops form NIC to vSwitch(UserSpace) to vNIC to vSwitch and back to NIC.
    - East-West Traffic(internal):
        - SR-IOV: Hops from vNIC to NIC to reach other vNICs (possible bottlenetcks)
        - DPDK: Hops from vNIC to vSwitch to reach other NICS.

1. Vector Packet PRocessing (VPP):
    - Beyond sequential pacet processing->process packets in batches(parallel)
    - Originally Cisco
    - High perfomance virtual switching
    - *VPP and DPDK good match*
2. Direct Memory Access (DMA):
    - A common shared area of Memory in the host is used as a mechanism to exchange data between VMs.
    - The memory space is treated as a PCI device
    - Isolation principle is broken!!!
    - Needs Hypervisor support.

# Networking Modes of Virtualbox
1. (Network address Translation) NAT Adapter:
    - Default in Vbox
    - Allows accesing the internet through Host, as if the guest is connected to a router.
    - Each Guest has its own NAT so they are not able to inter-communicate
    - Private Address
    - Not suitable for server unless port-forwarding is enabled.
    - Guest Invisible to the outside world.
2. Host-Only Adapter:
    - Allows communication between the Host and VMs
    - No connectivity to the outside world
    - New loopback interface on host
3. Bridge Adapter:
    - Traffic is filtered at the host NIC and injeted to/from Guest.
        * this emulates a virtual switch operation (bridging)
    - This allows connecting a VM with an external device directly over the physical NIC of the host.
    - A VM in bridged mode can be thought of as another machine in the LAN.
    - Servers as VMs
4. Internal Network:
    - Network visible to VMs connected to it but not to the host
        * You cannot debug/capture traffic from host!
    - Isolated
5. NAT Network:
    - Internal Network with NAT capabilities
    - Access to the outside world
