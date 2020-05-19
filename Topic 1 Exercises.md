# Topic 1 Exercises

## Make a brief list of applications that you use daily. For each of them:
- Consider a suitable Cloud Deployment Model. Explain
- Consider the Cloud Service Model they are (may be) base on. Explain

*Answer*

- Mail Service::
    - A suitable cloud deployment for a mail service is a Private Cloud. When you operate a mail service, either in-house either as a product(Gmail etc.) you are responsible for the integrity and the confidentiality of the data you  are managing, so you must be able to monitor and manage the underlying infrastrucure both physical (servers, and connection between servers and datacenters) as well as software(web services and database).
    - A mail service is based on a Software as a Service model. The main reason for that is that the user of that service just needs the ability to send, receive, and store mails, without managing and setting up the infrastructure needed for that.

- Cloud Computing::
    - The suitability of cloud deployment model for computing purposes depends on the confidentiality of the data involved. In general a public cloud deployment is fine for research purposes and for publically accesible data, but many enterprizes would prefer their data to stay on their own premises. In that case a Private Cloud is the preferred solution.
    - Cloud Computing services are based on IaaS. In cloud Computing services the customer has the ability provision the underlying hardware(number of CPUS, VMs, ram) and scale up to his needs.


## Consider a scenario where you would like/need to use VLAN-based virtual networks within an organization

*Answer* 

There are many cases, where you would like to use VLANs inside an organization. You may want a guest network for external visitors but would like to keep this separated from the rest of the netowrk. Also you may want to enforce different rules or policies to whole groups of devices or users, and it is easier to do it for a whole virtual network rather than for each specific case. 
