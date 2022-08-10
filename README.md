# Ansible Kubernetes Deployment
Ansible roles to install and configure a production Kubernetes environment.

Required nodes:
* OS: Ubuntu 20.04
* CPU: 2 CPU/2 Cores
* RAM: 8 GB
* HDD: 100 GB
* Subnet: 10.10.10.0/16

Hosts:
* Ansible-Controller - 10.10.10.254
* Master01 - 10.10.10.110
* Master02 - 10.10.10.111
* Master03 - 10.10.10.112
* K8-Cluster - 10.10.10.113 (virual IP on Master01)
* Worker01 - 10.10.10.210
* Worker02 - 10.10.10.211
* Worker03 - 10.10.10.212
* Gateway  - 10.10.0.1

Ansible command: ansible-playbook -v playbook1.yaml -t deploy_kubernetes
