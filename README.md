# Ansible Kubernetes Deployment
Ansible roles to install and configure a production Kubernetes cluster environment on a single node.

Required nodes:
* OS: Ubuntu 18.04.6 Server (Min Install)
* CPU: 2 CPU/2 Cores
* RAM: 8 GB
* HDD: 100 GB
* Subnet: 192.168.200.0/24

Hosts:
* Master01.lab.local - 192.168.200.101
* Cluster01.lab.local - CNAME

Ansible command: ansible-playbook -v playbook1.yaml -t deploy_kubernetes
