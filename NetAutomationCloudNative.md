# Net Automation and Cloud Native Design

## Explain the concept of network automation in the context of Cloud environments
In cloud environments:
 - multiple physical servers
 - multiple virtual entities
 - multiple networks connecting service components to one another and to the outside.
It is complex and cumbersome to carry out manula configurations in such an environments. Reconfigures VMs, replicas etc. Hence the need for automation.
Basic aims of network automation:
* Simplify setup, operation and management-> simples architectures, standarization of configurations
* Deterministic outcomes -> automation lead to predictable deterministic outcome which is not the case for manual configuration
*  Agility -> Ability to deploy / modify redeploy a service faster

### Types of Network automation
1. Device Provisioning: initial config and bootstraping
2. Data Collection: monitoring
3. Migrations: version or provider transitioning
4. Configuration Management: deploying, pushing and managing configuration state of devices
5. Compliance Validation: inputs/outputs
6. Reporting: generate reports from collected data
7. Troubleshooting: automatic problem identification and solution

Automation can be based on current documentation, and when done can serve as documentation itself.

## What is Ansible?
Decentrailized, agentless automation tool.
- SSH/TCP trasport protocoll
- Push model(can also pull)
- Python Based
- Jinja templating
- based on playbooks

## What kind of tool is it?
It is a configuration management tool:
- State description and enforcement
- Exposes domain specific language

It is based on scripting -> playbooks [hosts(target remote servers) + ordered list of tasks]
- SSH connection parallel for each host
- Executes tasks simultaneously in all hosts according to task list
- Push Model

* Requirements:
- Remote servers need ssh + python
- Control server need SSH + Python v2.6

Targets are set up in /etc/ansible/hosts and we can specify groups.
examples
{{
ansible targets -m command -a "ping dadsad"
}}

* Playbooks are written in YAML.
* Modules can bu used to perform different kind of actions on the host.
## What is Cloud Native Design?
It is an evolving definition.
Includes flexibility, scale automation, architecture and design.
It is basically a process of adoption of cloud methodologies:
## Which are its principles?
3 Pillars:
- Cloud Native Services
- Application centric design
- Automation

Application no longer as monoliths:
    - Microservices

### Design Consideration for Cloud Native Design
- Resiliency
- Parallelization (design application is such way to make parallelization of tasks possible - avoid sequential locks)
- Event-Drive perability: state based application design
- Instrumentation (observability/telemtry) : logs
- Security: multicomponent + a lot of it falls on the shoulder of the CLoud provider
- Agility and FutureProof: deployment , upgrade ,scale whould be fast and reliable

## Which are its implications?
Development and Operation teams merged into DevOPS
clear defined interfaces, APIs
Team-ownership in all phases:
- small, multidisciplinary teams both in team and individual level.
