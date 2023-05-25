Kubernetes Microservice App


Docker
```
* docker build -t username/tag:latest .
* docker push username/tag:latest

```


Kubeadm Installation

Both Master & Worker Node
```
sudo su
apt update -y
apt install docker.io -y

systemctl start docker
systemctl enable docker

curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg
echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' > /etc/apt/sources.list.d/kubernetes.list

apt update -y
apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y

```

To connect with cluster execute below commands on master node and worker node respectively

Master Node

```
* sudo su
* kubeadm init

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  
* kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

* kubeadm token create --print-join-command

```
  

Worker Node

```
* sudo su
* kubeadm reset pre-flight checks
* Paste the Join command on worker node and append `--v=5` at end

```


#To verify cluster connection  

on Master Node
```
* kubectl get nodes 

```
