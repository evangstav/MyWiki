# Exercise Lecture 2

1) Consider a standard 3 tier DC architecture with *2* core switches attached to a total of *10* aggregaton switches. Each aggregation switch is attached to *20* ToRs, with 20 servers per rack. The hypothetical link delays are:
    - Core-Aggregation = 0.1 ms
    - Aggregation-ToR = 0.2 ms
    - Tor-Host = 40 ms
    i) What is the end to end North-South delay in the DC, from core switch to host?
        *Answer*
        The e2e North-South delay is::
            e2eNS = Tor-Host + ToR-Aggregation + Core-Aggregation = 42,1 ms
    ii) What is the maximum East-West e2e delay in the DC between hosts?
        *Answer*
        The maximum e2e East-West delay is from a given host all the way to the core switch and then to the other host.
        So 2*e2eNS = 84,2 ms
    iii) What in the minimum East-West e2e delay in the DC between hosts?
        *Answer*
        The minimum e2e East-West delay is when the hosts are in the same rack.
        So 2*Tor-Host = 80ms
    
2) A possible solution to this problem would be using VXLAN. Utilizing VXLAN tags we can provide the the needed isolation, while allowing the tenant with their own mac address pool.  
   
Where you would terminate VXLAN?
*The easiest would be to do that in the core node. But it depends on the amount of tenants. With many tenants you will do that at the ToR.* So it depends!
