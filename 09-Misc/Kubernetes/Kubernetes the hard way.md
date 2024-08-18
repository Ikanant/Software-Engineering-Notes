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

Getting all 4 VMs running took a bit and one thing to keep in mind is that ssh(ing) into all at once using multiple VS Code windows does require to tweak my ssh config a bit:

![[Pasted image 20240818115850.png]]

By the end of it all I got this:
![[Pasted image 20240818120024.png]]


One thing I forgot to account for is that these VMs need to be able to communicate with one another... which the way I have it setup right now in virtual box won't really allow. I created them all with a NAT connection (which is default) and I was just port forwarding things in... INSTEAD what I should have done (I now tested) is in Virtual Box create a NAT Network myself:
![[Pasted image 20240818124620.png]]
And then have each VM use that:
![[Pasted image 20240818124642.png]]

In this case I specified my IP and Subnet as 10.0.4.0 for example and after restarting each VM they now have been assigned an IP in that range. which ultimately looks like .4 .5 .6 .7. Same as before I added the Port Forwarding roles here for ports 3022 3023 3024 3025 and VS Code from my host machine was able to once again connect to each VM using SSH...

Moment of truth, I pinged one of the VMs from inside another... and got a response back. I am ready to continue with Kubernetes setup now.