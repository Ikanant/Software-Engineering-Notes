https://github.com/kelseyhightower/kubernetes-the-hard-way

* Setup first VM using Debian 12 - Bookworm. Documentation above is meant to be used in an arm64 architecture but I rather spin everything up in my windows machine. So all URLs found for my kubectl server were switch accordingly:

https://dl.k8s.io/v1.31.0/bin/linux/amd64/kube-apiserver
https://dl.k8s.io/v1.31.0/bin/linux/amd64/kube-controller-manager
https://dl.k8s.io/v1.31.0/bin/linux/amd64/kube-scheduler
https://dl.k8s.io/v1.31.0/bin/linux/amd64/kube-proxy
https://dl.k8s.io/v1.31.0/bin/linux/amd64/kubelet
https://github.com/kubernetes-sigs/cri-tools/releases/download/v1.31.1/crictl-v1.31.1-linux-amd64.tar.gz
https://github.com/opencontainers/runc/releases/download/v1.1.13/runc.amd64
https://github.com/containernetworking/plugins/releases/download/v1.5.1/cni-plugins-linux-amd64-v1.5.1.tgz
https://github.com/containerd/containerd/releases/download/v1.7.20/containerd-1.7.20-linux-amd64.tar.gz
https://github.com/etcd-io/etcd/releases/download/v3.5.15/etcd-v3.5.15-linux-amd64.tar.gz

![[Pasted image 20240818104015.png]]

In order to make my life easier I just made sure VM allows for SSH exposing the port 22 in the machine to be routed through 3022 in my host. Connecting it's as simple as:

> ssh -p 3022 ikakant@127.0.0.1

One quick reminder for myself... ensure VM has openssh-server package otherwise things won't work:
> sudo apt-get install openssh-server
