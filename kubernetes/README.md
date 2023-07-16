# Kubernetes Deployment using kubeadm

This guide explains the steps to set up a Kubernetes cluster using `kubeadm` on a master node and worker nodes.

## Prerequisites

- Linux-based operating systems (e.g., Ubuntu, CentOS) for both master and worker nodes.
- Port range 0-65535 open on all nodes.

## Installation Steps

### On Both Master and Worker Nodes

1. SSH into each node as root or execute the following command to switch to root:

```bash
sudo -i
```

2. Update the system:

```bash
yum update -y
```

3. Disable swap:

```bash
swapoff -a
```

4. Disable SELinux:

```bash
setenforce 0
```

5. Install Docker:

```bash
yum install docker -y
systemctl start docker
systemctl enable docker
systemctl status docker
```

6. Add Kubernetes repository:

```bash
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=0
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kube*
EOF
```

7. Configure kernel parameters:

```bash
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```

8. Install Kubernetes components:

```bash
yum install -y kubeadm-1.21.3 kubelet-1.21.3 kubectl-1.21.3 --disableexcludes=kubernetes
systemctl start kubelet
systemctl enable kubelet
systemctl status kubelet
```

### On Master Node Only

9. Initialize the Kubernetes cluster:

```bash
sudo kubeadm init --apiserver-advertise-address=<master-node-ip> --pod-network-cidr=192.168.0.0/16 --ignore-preflight-errors=NumCPU --ignore-preflight-errors=Mem
```

Replace `<master-node-ip>` with the IP address of the master node.

10. Set up the Kubernetes configuration:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

11. Install a network plugin (e.g., Calico):

```bash
sudo kubectl apply -f https://docs.projectcalico.org/v3.3/getting-started/kubernetes/installation/hosted/rbac-kdd.yaml
sudo kubectl apply -f https://docs.projectcalico.org/v3.8/getting-started/kubernetes/installation/hosted/kubernetes-datastore/calico-networking/1.7/calico.yaml
```

12. Verify the configuration:

```bash
kubectl get pods --all-namespaces
```

13. Generate a new token for joining worker nodes:

```bash
kubeadm token create --print-join-command
```

14. Check the nodes:

```bash
kubectl get nodes
kubectl describe nodes
```

### On Worker Nodes Only

15. Join the worker nodes to the cluster:

```bash
kubeadm join <master-node-ip>:6443 --token <token> --discovery-token-ca-cert-hash <hash>
```

Replace `<master-node-ip>` with the IP address of the master node, `<token>` with the generated token, and `<hash>` with the discovery token CA certificate hash.

16. Verify the node join status on the master node:

```bash
kubectl get nodes
```
