
# easy-kubernetes

Firewalld for Master 
```bash
systemctl restart firewalld
systemctl enable firewalld
firewall-cmd --permanent --zone=public --add-port=80/tcp
firewall-cmd --permanent --zone=public --add-port=443/tcp
firewall-cmd --permanent --zone=public --add-port=4443/tcp
firewall-cmd --permanent --zone=public --add-port=6443/tcp
firewall-cmd --permanent --zone=public --add-port=2379-2380/tcp
firewall-cmd --permanent --zone=public --add-port=10250/tcp
firewall-cmd --permanent --zone=public --add-port=10251/tcp
firewall-cmd --permanent --zone=public --add-port=10252/tcp
firewall-cmd --permanent --zone=public --add-port=10255/tcp
firewall-cmd --permanent --zone=public --add-port=8472/udp
firewall-cmd --zone=public --add-masquerade --permanent
# only if you want NodePorts exposed on control plane IP as well
firewall-cmd --permanent --zone=public --add-port=30000-32767/tcp
firewall-cmd --reload
systemctl restart firewalld
```

Firewalld for Worker
```bash
systemctl restart firewalld
systemctl enable firewalld
firewall-cmd --permanent --zone=public --add-port=80/tcp
firewall-cmd --permanent --zone=public --add-port=443/tcp
firewall-cmd --permanent --zone=public --add-port=4443/tcp
firewall-cmd --zone=public --permanent --add-port=10250/tcp
firewall-cmd --zone=public --permanent --add-port=10255/tcp
firewall-cmd --zone=public --permanent --add-port=8472/udp
firewall-cmd --zone=public --permanent --add-port=30000-32767/tcp
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --reload
systemctl restart firewalld
```

Setup a Kubernetes v1.18 cluster easily on CentOS 8.1 in VmWare

1. Add Your SSH Public key(cat ~/.ssh/id_rsa.pub in Local mechine) under the server ~/.ssh/authorized_keys

2. Install Ansible in your local mechine.

3. Change the Master, worker nodes IP Adds in /inventories/main.ini

[kubernetes_master]
192.168.0.157
192.168.0.158
192.168.0.159

[kubernetes_nodes]
192.168.0.170
192.168.0.171

[kubernetes_haproxy]
192.168.0.157
192.168.0.158
192.168.0.159

[kubernetes_servers:children]
kubernetes_master
kubernetes_nodes


## Overview

This system uses Docker container runtime


`ansible-playbook create-cluster-playbook.yml -b --user=root`
