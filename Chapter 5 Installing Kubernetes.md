# Chapter 5 Installing Kubernetes
- Four major installation types
	- All-in-One Single-Node Installation
		- All the master and worker components are installed and running on a single-node
		- Minikube
		- For learning, dev, testing
		- Not for prod!
	- Single-Node etcd, Single-Master and Multi-Worker Installation
		- Master node runs etcd instance
		- Multiple worker nodes connected to master node
	- Single-Node etcd, Multi-Master and Multi-Worker Installation
		- Multiple master nodes in HA mode
		- Single-node etcd instance
		- Multiple worker nodes connected to the master nodes
	- Multi-Node etcd, Multi-Master and Multi-Worker Installation
		- Recommended
		- Etcd nodes in HA mode
		- Master nodes in HA mode
		- Multiple worker nodes to master nodes


#kubernetes/edxIntroToKubernetes/chapter5
#pivotal/flexhour