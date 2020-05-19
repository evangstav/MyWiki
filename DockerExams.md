# [Docker](Docker.md)

## What is a Container?
Container describes a modified runtime environment, that isolates processes run within it from all resources except from those specifically allowed.
* *Machine Container*: closer to a VM
    - Designed to run mulitple processes and applications
    - Have their own init process and a number of daemons
    - Allow program installation and configureation
    - *They do not run their own kernel*, only some daemons and additional files.
* *Application Container*:
    - Designed to package a single application
    - No shell, or init process
## How does it compare with a VM?
* Container are much "lighter":
    - No HW virtualisation
    - No additional OS
    - reduced overhead and resource requirements
* Containers isolate apps:
    - independency, no cross-impact
    - VMs tend to group different apps in a single VM -> dependencies and performance impact (resource economy)
    - Containers share the same kernel -> less secure!!

## What are the enablers for container technology?
Two mechanisms make this possible:
1. [Linux Namespaces](VirtualizationSupportInLinux.md) allows for each process to see its own view of all system resources.
3. *Linux Control Groups* provides a way to control and limit the amount of resources a process can consume.

## What are images and layers in the context of container technology?
- Image: The sum of files that should be available to the application running in the container.
- Layers: A docker image consists of several layers. Each layer corresponds to certain instructions in the DockerFile(RUN, COPY, ADD). So layers are the components of an image. Eg.:
    * addtions to OS
    * additional files configs etc.
    * Metadata like paths, env variables.
## What is Docker?
Docker is a container runtime application. It hides and automatize the underlying OS mechanisms enabling the creation and administration of containers. It is a CLI program, a daemon and a set of remote services.
## How are containers interconnected by default in Docker
Containers by default use bridge connectivity. In that mode all containers are accesible to each other.
- Common network for all containers in the host.
- All containers have access to each other(*consider -icc flag for inhibiting this when initiating the daemon->usefull for multitenancy*) 
- Ad-hoc bridges:
    * Separate networks within the host, isolated from each other
## Explain other variants of Docker container connectivity.
- Closed Container:
    - only local traffic-> lo
    - no external connectivity->most secure
    - for applications that require no external connectivity

- Joined Container:
    - Reuses the network namespace of another container -> they share the net stack and interfaces
    - *WARNING* Potential port conflict issues

- Open(Host) Container:
    - Full access to the Host network and Host's network services.
        - Dangerous!!


## What is the Containers Network Model (CNM)?
CNM is a container networking standard proposed by Docker. It has interfaces for both IP Adress Management (IPAM) and network plugins. 
- IPAM plugin can be used to create/delete address pools and allocate/deallocate IP@s
- network plugin can be used to create/delete networks and add/remove containers from networks.
*libnetwork* defines an API compliant with CNM, implemented in GO. Docker uses libnetwork to create/manage networks within a host or among hosts.


