# Chapter 6 A Local Single-Node Kubernetes Cluster
- Minikube
	- builds all its infrastructure as long as a Type-2 Hypervisor (VirtualBox, etc.) is installed
	- invokes the Hypervisor to create a single VM which then hosts a single-node K8 cluster
- Prereq setup:
	- [Install and Set Up kubectl - Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
	- [Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
		- Alternatives: (linux) KVM, (macOS) HyperKit, VMware Fusion, (Windows) Hyper-V
	- VT-x/AMD-v virtualization must be enabled on the local workstation in BIOS
- Install VirtualBox (bionic Ubuntu 18.04)
```
$ sudo bash -c 'echo "deb https://download.virtualbox.org/virtualbox/debian bionic contrib" >> /etc/apt/sources.list'
$ wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
$ sudo apt-get update 
$ sudo apt-get install -y virtualbox-6.0
```
- Install Minikube
`$ brew cask install minikube`
- Start && check status && stop Minikube
`minikube start`
	`minikube start —vm-driver=virtualbox`
	`minikube config set vm-driver virtualbox` 
	(make VB the default driver)
`minikube status`
`minikube stop`

