```
https://www.youtube.com/watch?app=desktop&v=8k2PfMHQnt4

sudo apt-get install -y containerd

sudo su -
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

apt-get update
apt-get install -y kubelet kubeadm kubectl
apt-mark hold kubelet kubectl containerd

swapoff -a
vi /etc/fstab
comment the swap line
```
