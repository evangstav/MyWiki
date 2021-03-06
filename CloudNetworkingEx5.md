# Exercise Topic 4

1) VBox Cli
    a) We can list all available virtual machines in the terminal by:
                - VBoxManage list vms
    b) We can list the internal networks managed by virtual box via:
        - VBoxManage list itnets
    c) We can create new NAT network by:
        - VBoxManage natnetwork add --netname <networkname> --network <network>
    
    We tested it by attaching two minimal vms to it and pinging the internet from them.
    
2) In the proposed network architecture with assume that we as provider must not have access to any of the guest subsystems. If not we could replace all internal interfaces with host-only. So for the proposed architecure:
    1) FrontEnd WS : 2 interfaces, a bridged and an internal(int1).
    2) BackEnd WS: internal(int1), possibly host-only for ext. management.
    3) DB server: internal(int1)
    4) Streaming Server: Bridged (or int1 if we want acces through the front WS instead of from the outside), internal(int2)
    5) internal(int2)

The main ideas behind the above proposal is that our webserver and possibly the streaming server would require outside IP addresses in order to be easily accesible from the outside. The FE and the SS are also connected to the DB and the FS respectively using the internal interfaces int1, int2. That is required for security reason since our DBs and FServers should not be visible to the outside. Lastly the BE is connected to both int1 and int2 in order to effectively monitor all parts of the network, and a host only interface could be usefull for some external modification( but possibly compromises security, so it would be better deployed in an in-house solution. )

    b) SR-IOV could be used in order to improve the perfomance of the FrontEnd WS as it would allow faster perfomance for the outside connections. For the SServer it would not be a good solution given the amount of streaming data, as it rsiks bottleneching the pci-bus. For the int1 given the amount of reads and writes to the DB from both BE and FE it would be beneficial to use DPDK.



