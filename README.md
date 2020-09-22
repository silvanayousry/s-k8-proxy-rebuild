# Purpose

Building a K8s cluster using a portable option to be used across any cloud providers or on-prem machines.

There are multiple ways and tools to implement K8s including:

  ### Learning environment:

   - [minikube](https://kubernetes.io/docs/setup/learning-environment/minikube)

   - [kind](https://kubernetes.io/docs/setup/learning-environment/kind)

   - [k8s the hard way](https://github.com/kelseyhightower/kubernetes-the-hard-way)

  ### Production environment:

   - [kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm)

   - [kops](https://kubernetes.io/docs/setup/production-environment/tools/kops)

   - [kubespray](https://kubernetes.io/docs/setup/production-environment/tools/kubespray).

  ### Third party tools:

   - [microk8s](https://microk8s.io)

# Kubernetes deployment

## kubespray

Kubespray is a composition of Ansible playbooks that helps to install a Kubernetes cluster hosted on GCE, Azure, OpenStack, AWS, vSphere, Packet (bare metal), Oracle Cloud Infrastructure (Experimental) or Baremetal.

### Requirements

1- Ansible v2.9 and python-netaddr is installed on the machine that will run Ansible commands.

2- Jinja 2.11 (or newer) is required to run the Ansible Playbooks.

3- The target servers must have access to the Internet in order to pull docker images.

4- The target servers are configured to allow IPv4 forwarding.

5- Your ssh key must be copied to all the servers part of your inventory.

6- The firewalls are not managed, you'll need to implement your own rules the way you used to. in order to avoid any issue during deployment you should disable your firewall.

7- If kubespray is ran from non-root user account, correct privilege escalation method should be configured in the target servers. Then the ansible_become flag or command parameters --become or -b should be specified.

### Installation

1- The VMs running K8s will be hosted on GCP with the following specs:

- 1 Bastion, 1 master and 1 worker
- Ubuntu 18.04
- e2-medium (2 vCPUs, 4 GB memory)

2- Generate a new ssh-key on the bastion and copy it to authorized_keys of all the machines:

  `ssh-keygen`

2- Install needed packages on the bastion server:

```
sudo apt update
sudo apt install ansible python3-pip
git clone https://github.com/kubernetes-sigs/kubespray.git
cd kubespray/
sudo pip3 install -r requirements.txt
```

3- Build the inventory file ([ansible](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/ansible.md)):

```
[all]
node1 ansible_host=$IP  ip=$Internal_IP
node2 ansible_host=$IP  ip=$Internal_IP


[kube-master]
node1

[etcd]
node1

[kube-node]
node2

[k8s-cluster:children]
kube-master
kube-node
```