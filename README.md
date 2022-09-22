# Ansible Kubernetes Deployment
Ansible roles to automatically install, configure & deploy a production Kubernetes cluster environment on a single node using kubeadm.

Required nodes:
* OS: [Ubuntu 18.04.6 Server (Min Install)](https://releases.ubuntu.com/18.04/)
* CPU: 2 CPU/2 Cores
* RAM: 8 GB
* HDD: 80 GB
* Subnet: 192.168.200.0/24
* Hostname: master01.lab.local
* Software: openssh-server, ansible 2.5.1, python 2.7.17 

Hosts:
* master01.lab.local - 192.168.200.101
* cluster01.lab.local - CNAME

* Ansible command: $ ansible-playbook -v playbook1.yaml -t deploy_kubernetes
* Revert command:  $ ansible-playbook -v playbook1.yaml -t reset_cluster

* Once Ansible is complete, run command: $ kubectl get pods --all_namespaces
* Follow guidance [here](computingforgeeks.com/join-new-kubernetes-worker-node-to-existing-cluster/) to join additional master & worker nodes to the cluster
 
# Pre-Configuration Settings:
* Set static IP of server to 192.168.200.101/24 (You can change this but be sure to change the IP variable in vars/all)
* Ensure /etc/hosts has an entry for 127.0.1.1 master01, 192.168.200.101 master01.lab.local master01 cluster01.lab.local cluster01
* Comment out swap mount in /etc/fstab and reboot server
* Create a user "ansible" and ensure user is part of the sudo group
* Edit /etc/sudoers %sudo line.  Change line to ALL=NOPASSWD: ALL
* Create ssh key by running the command: $ ssh-keygen -t rsa (accept all defaults) 
* Then run command: $ ssh-copy-id ansible@master01.lab.local
* Touch a file called /var/log/ansible.log and run command: $ chown ansible:sudo /var/log/ansible.log
* Test ansible by running the command: $ ansible -m ping all
