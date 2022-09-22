# Ansible Kubernetes Deployment
Ansible roles to automatically install, configure & deploy a production Kubernetes cluster environment on a single node.

Required nodes:
* OS: [Ubuntu 18.04.6 Server (Min Install)](https://releases.ubuntu.com/18.04/)
* CPU: 2 CPU/2 Cores
* RAM: 8 GB
* HDD: 100 GB
* Subnet: 192.168.200.0/24
* Hostname: master01.lab.local
* Software: openssh-server, ansible 2.5.1, python 2.7.17 

Hosts:
* Master01.lab.local - 192.168.200.101
* Cluster01.lab.local - CNAME

Ansible command: $ ansible-playbook -v playbook1.yaml -t deploy_kubernetes
* Once Ansible is complete, run command: $ kubectl get pods --all_namespaces
* Expected Result:
* NAMESPACE          NAME                                       READY   STATUS    RESTARTS   AGE
* calico-apiserver   calico-apiserver-5bb6748454-5qtqb          1/1     Running   0          34m
calico-apiserver   calico-apiserver-5bb6748454-f264n          1/1     Running   0          34m
calico-system      calico-kube-controllers-85666c5b94-cf446   1/1     Running   0          35m
calico-system      calico-node-l4r6h                          1/1     Running   0          35m
calico-system      calico-typha-7b5c5d64c7-hkdv2              1/1     Running   0          35m
calico-system      csi-node-driver-nkk94                      2/2     Running   0          34m
kube-system        coredns-565d847f94-chctt                   1/1     Running   0          35m
kube-system        coredns-565d847f94-ctmpw                   1/1     Running   0          35m
kube-system        etcd-master01                              1/1     Running   0          35m
kube-system        kube-apiserver-master01                    1/1     Running   0          35m
kube-system        kube-controller-manager-master01           1/1     Running   0          35m
kube-system        kube-proxy-6f7kk                           1/1     Running   0          35m
kube-system        kube-scheduler-master01                    1/1     Running   0          35m
tigera-operator    tigera-operator-6675dc47f4-8kxrm           1/1     Running   0          35m

# Pre-Configuration Settings:
* Set static IP of server to 192.168.200.101/24 (You can change this but be sure to change the IP variable in vars/all)
* Ensure /etc/hosts has an entry for 127.0.0.1 master01, 192.168.200.101 master01.lab.local master01 cluster01.lab.local cluster01
* Comment out swap mount in /etc/fstab and reboot server
* Create user ansible and ensure user is part of the sudo group
* Edit /etc/sudoers %sudo line.  Change line to ALL=NOPASSWD: ALL
* Create ssh key by running the command: $ ssh-keygen -t rsa (accept all defaults) 
* Then run command: $ ssh-copy-id ansible@master01.lab.local
* Touch a file called /var/log/ansible.log and run command: $ chown ansible:sudo /var/log/ansible.log
* Test ansible by running the command: $ ansible -m ping all
