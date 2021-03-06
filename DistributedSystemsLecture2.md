# Distributed Systems Lecure 2


## Physical Models
### Baseline
### Early distributed

## Architectural vs Fundamental Models
- Systems
- Architectures
- Fundamental Models

### Architectural Model
4 fundamental blocks::

1) Communicating Entities
    - Systems Perspective
    - Programming Perspective
2) Communication  Paradigms
    1) Direct 
        - interprocess communication
        - remote invocation
    2) Indirect
        - group
        - publish
        - message queue
        - tuple space
        - DSM
3) Roles & Responsibilities
    1) Client-Server Model
        - Requests
        - Replies
        - Invoke Invocation
    2) Peer to Peer model
        - similar roles
        - resources are shared
        - Data/Process replication 
4) Placement Strategies
    1) Mapping of services to miltipleservers
    2) Proxy server and cache
    3) Mobile Code::
        - Client requesting code running on device and get the results locally
        - good interactive responce
        - security??
        - computational restrictions

### Fundamental Models
1) Properties 
2) Characteristics

#### Assumptions on interacting processes
- rate at which each process proceeds
- timing of 
- states
- private states

#### Factors Affecting Interacting Processes
1) Communication Perfomance
    - Latency
    - Bandwidth
    - Jitter
2) Timing

#### Interaction Model
1) Synchronous::
    - Assumptions about time...
2) Asynchronous::
    - No asumptions about time...
    - No global clock

## Design Challenges
### Heterogenesity
    - variety and differences in::
        - networks
        - hardware
        - op.sys
        - programming languages
        - implementations
    - Can be adresses by:
        - protocols(eg. Internet Protocols)
        - middleware( software layer/interface abstraction )
### Transpaency
    - The distributed system is perceived as a whole rather than a collection of components.
    - 
### Openness
Can be extented and reimplemented.


### Concurrency
### Security
- Confidientality 
- Integrity
- Availability
 
### Scalability
Designed to remain effective when there is a significance increase in the number of resources and users.


### Resilience to Failure
- Partial Faillures
#### Failure Model
Types::
    - Omission 
    - Arbirtary (Byzantine??)
    - Timing


#### Thin Client vs Thick Client
thin:   presentation                         <- application processing, data management
thick:  presentation, application processing <- data management
