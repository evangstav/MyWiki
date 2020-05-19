# Exercises Topic 5

1. Information flows
    - (FEWS <- userplaylist, available content -> DB)
    - (BEWS <- user-preferences, FE configuration, user-recomendations -> DB)
    - (FEWS <- user creds -> outside)
    - (BEWS <- Front End configuration -> FEWS)
    - (FS -> content stream -> SS)

2. Information flows are enabled by the MANO and specifically by its Virtual Infrastructure Managers (VIM).

3. After the virtual machine is initialized the VIM should report back to NFVO the the VM is available. THen NFVO notifies VNFM and VNFM configures the FE VNF. Then VNFM informs the NFVO tha FE is available for use and our system is up and running.


