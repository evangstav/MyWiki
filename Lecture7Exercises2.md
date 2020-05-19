=Topic 6b Exercises=

1. While logged in as demo user i could not create any new users.
2. On the other hand while connected as admin I could create new users. Additionaly I could see every user unlike when I was connected as "demo".
3. As admin:
    1. name
    2. status
    3. Net ID
    4. 2 subnet IDs
    5. 2 corresponding  IP Addresses
    6. all 3 interfaces
    As user "demo" I could see only the 2 "internal" interfaces but not the external gateway.
    
4. KVM:
    1. Using virsh command net-list on the vm running openstack I could only see 1 network. Also by using net-dumpxml we get information about this network. We can see that a linux bridge named virbr0 is instanciated with an ip adress 192.168.122.1/24. We can see that a dhcp server is handing i addresses in the range 192.168.122.2-192.168.122.254. Openstack manages the network independently from kvm.
    
5. I should be able to capture traffic related to DHCP leases in the respective qdhcp tap interfaces. Unfortunately I could not try it since my machine kept on crashing. Putting the interface up and down again from inside the VM. 
   
6. Capturing Openstack Traffic
- In the hosting machine we can use tcpdum -i lo port http (loopback interface)
- Look at firewall default ports

