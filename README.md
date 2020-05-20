#Setup a Kubernetes v1.18 cluster easily on CentOS 8

## Overview

This project intends to show how easy it is to setup a K8s cluster with minimal experience using Kubnernetes. I have adapted this project from the great guide: [Installing Kubernetes on Linux with kubeadm](http://kubernetes.io/docs/getting-started-guides/kubeadm/)


### Installation

3x master
2x nodes

In your [inventory](./inventories/main.ini) place the IP addresses you intend to use.

Now you can provision your K8s cluster with:

`ansible-playbook create-cluster-playbook.yml -b --user=root`


