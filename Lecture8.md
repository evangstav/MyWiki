# Docker

Evolution:

- Monolithic 
- Distributed
- Microservices
 
## Containers vs VMs
- Images:
    - Sum of files required for the application running in the container
- Layers: Components of an image::
    - Os additions
    - file additions
    - Metadata

## Basic Docker Commads
list images: sudo docker image ls -a
run container: sudo docker run [y](--interactive]] [[--tt.md) --name client busybox:latest /bin/sh
detach: CTRL-P-Q
attach: docker attach name
access to log information: docker logs -t name
resource usage: docker stats name
pause: docker pause name
restart: docker unpause name
stop: docker stop name
remove: sudo docker rm name (with -v to delete volume)

## Docker Registries
A Docker registy is a repository for Docker Images. Docker Clients connect to registries to pull images to use, or to push images that they have built. Registries can be public or private. Two main puplic registries are Docker Hub and Docker Cloud. Docker is the default registy where Docker looks for images.

## Docker as Container exec Environment

## Docker Networking
Docker allows different network configurations.
- Bridged Container:
    - Default:
        - Common network for all containers in the host.
        - All containers have access to each other(*consider -icc flag for inhibiting this when initiating the daemon->usefull for multitenancy*) 
    - Ad-hoc bridges:
        - Separate networks within the host, isolated from each other

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

## Firewalling
- Containers are firewalled from the outside by the host.
- Docker provides mechanisms to map container ports to the HOST interface at instantiation, so that they can be reached from the outside: run .. -p <>:<>. Different patterns are possible:
    - <HostIP@>:<HostPort>:<container port>
    - <HostIP@>::<container port>
    - <HostPort>:<container port>



### Bridged Container
- Docker Bridge -> Security issue
- By default all containers are interconnected: there is a veth interface for each container to a bridge instantiated on the host.
- For security reason docker does not add the containers network namespace to run time. We can add it by finding the Pid with *docker inpect name* and then on host running: sudo ln -sf /proc/<Pid>/ns/net "/var/run/netns/client" 
# Exercises Tips
[|Exercises](Lecture8Exercises.md)

# Part 2

What if I want to create multiple container-network within a single host?
- create a new network: sudo docker network create myNT -> actually creates a new linux bridge
- launch container in specific net by using the --net FLAG
- it is also possible to configure bridges at creation by using --ip-range nad --subnet flags. E.g :
    - sudo docker network create --ip-range "10.0.10.0/24" --subnet "10.0.10.0/24" mine
- We can also configure the default docker bridge by creating a json with bip and mtu values like:
- ``` json
    {
    "bip":"192.168.1.7/24",
    "mtu":1200,
    }
    ```
- we can achieve the same results by initiating the docker daemon with --bip and mtu flags

## Docker Swarm
We are creating a docker swarm wth 2 hosts.



What is a docker swarm?
What are its components?
How are docker services exposed in doclker swarm?

Can I manage Docker containers using openstack?


### Exercises Part2

[|Exercises](Lecture8ExercisesPart2.md)
