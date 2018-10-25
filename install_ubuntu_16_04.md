# Setup on Ubuntu 16.04 VM's

## Master Node

```swapoff -a
apt-get update && apt-get upgrade -y
apt-get install -y docker.io
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg \
| apt-key add -
apt-get update
apt-get install -y \
kubeadm=1.11.1-00 kubelet=1.11.1-00 kubectl=1.11.1-00

kubeadm init --pod-network-cidr 192.168.0.0/16

As normal
 mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

wget https://goo.gl/eWLkzb -O calico.yaml
kubectl apply -f calico.yaml

kubectl taint nodes --all node-role.kubernetes.io/master-
source <(kubectl completion bash)
```

## Worker Node

```swapoff -a
apt-get update && apt-get upgrade -y
apt-get install -y docker.io
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg \
| apt-key add -
apt-get update
apt-get install -y \
kubeadm=1.11.1-00 kubelet=1.11.1-00 kubectl=1.11.1-00
```

Then run the join command from the output od the kubeadm init command on the master