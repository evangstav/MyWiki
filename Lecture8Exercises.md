# Exercises Topic 7a

## Docker hub
a) Network Monitoring
b) Network Visualization
c) Routing: TraefikEE
d) Load Balancer: super6awspoc/loadbalancer
e) Web Hosting: Oracle WebLogic
f) Database: MongoDB, MySQL
g) Media Streaming: streams
h) LTE's eNB: omecproject/lte-softmodem
i) LTE's EPC: openairinterface/epc


2. Is this all free??
No there are also subscription based containers, possibly offering free trials.

3. Is there any risk?
There is a bit less risk that running any other open source software. Docker offers some namespace protection but the application still use the same kernel so damage can be done. It is a bit safer to use official images from dockerhub, but they usually require a premium.

4. Both Vms and Containers have their own ares of applicability. VMs are great for running multiple applications together, or if we need complete logical isolation at the hardware level between services. Also due to this kind of isolation they are prefered when scurity is the primary concern. Containers on the other hand containers are great for micorservices, or applications that we want to run multiple copies of them at the same time.
