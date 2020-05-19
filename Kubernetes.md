# Kubernetes
[e](MiniKub.md)
    - Pods
    - Services

## [|Examples](K8s_examples.md)
## Architectural Components
Pods: Containers
Services: By default containers are not accesible outside the kubernets virtual network. In order to make the container availabe to the outside world you got to expose the Pod as a K8s service.

## Networking
Minikube seem to have created a veth interface connected to docker0. After "minikube ssh" I can see all interfaces from the nodes. I am not sure yet how they are connected to the brigde yet.

## Container Netowork Interface
The CNI allows Kubernetes to be configured to use any CNI plugin, like:
- Calico
- Flannel
- Romana
- Weave Net
- Others

## Scheduling
- The scheduler operation is based on a 2-step process:
    1. Filter the list of nodes to find the subset of nodes the POD can be scheduled to
    2. Choose the best node according to some prioritization policy. If multiple are euqally good:
        - round-robin policy -> even distribution

- It is possible to assign different schedulers per POD "shedulerName property"
    - If not set -> default

## Services
The service is represnted by a pair (IP@:port) that is used by the IPTablesof the Node to route the corresponding (real) IP and port of a running POD. The IP@ of the service is therefore "not-real" in a sense that it no attached to a physical device. Therefore it cannot be pinged.


## Discovering Services
- By default every new connection is sent to a randomly chosen POD in the service.
- It is possible to configure that all requests from the same client go to the same POD:
    - "sessionAffinity: ClientIP" (in spec group within the manifest file.)

But how tdo we know the IP@ of the service? There are two ways to do it in Kubernetes.
- Environmental Variables
- DNS

=== Service Discovery based pn Env Variables (EVs)===
- By default, every new connection is sent to a randomly POD in the service.
*It is possible to configure that all request from the same client go to the same POD: "sessionAffinity: ClientIP", in spec group within the manifest.yaml*

*Service Discovery*:
- At POD creation K8s initializes EVs for the POD, related to active services at this point.
- To check it out: kubectl exec "POD-name" env



### Service Discovery with DNS
- K8s uses a namespace concept to isolate resources
- If we "kubectl get po --namespace kube-system" we see some PODs related to DNS.
- These DNS PODS run DNS servers which other PODs in the cluster are configured to use:
    - /etc/resolv.conf file in each container
    - Configurable through the dnsPolicy property ina POD's spec.

## Accesing services from Outside
There are three mechanisms in K8s to enable external accesibility to a service:

- Service type ass *NodePort*: the nodes open a dedicated port and redirect traffic arriving on that port towards the related service.
- Service type as *LoadBalancer*: extension of NodePort; K8s creates a LoadBalancer which receives the requests to its IP@ and forwards to the corresponding NodePorts for the service in the nodes.
- Creating an *ingress resource*: HTTP level mechanism that allows to expose multiple Services through a single IP@.

### NodePort-based Service
### LoadBalanced-based service
### Ingress Based Service


[9](CloudNetworkingExercises.md)
