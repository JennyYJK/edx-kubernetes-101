# Chapter 7 Accessing Minikube
- `kubectl`  Kubernetes CLI client
	- manage cluster resources and applications
	- deploy apps, manage/configure K8s resources
- Kubernetes Dashboard - Web UI
	- interact with a K8s cluster to manage resources and containerized apps
- API server
	- On master node
	- CLI and Web UI connects to it
![](Chapter%207%20Accessing%20Minikube/Screen%20Shot%202019-08-17%20at%2012.47.52%20PM.png) http API Space of Kubernetes
	- Core Group (/api/v1)
		- pods, services, nodes, namespaces, configmaps, secrets, etc.
	- Named Group (/apis/$NAME/$VERSION)
		- version imply different levels of stability/support
		- Alpha level (/apis/batch/v2alpha1)
			- It may be dropped at any point
		- Beta level (/apis/certificates/v1beta1)
			- Well-tested, but subject to change
		- Stable level (/apis/networks/v1)
			- released software
	- System-wide
		- `/healthz` `/logs` `/metrics` `/ui`

- Installing kubectl on macOS
	- `brew install kubernetes-cli`

- Kubectl Configuration File
	- `~/.kube/config`
	- `kubectl config view`
	- `kubectl cluster-info` 

- Kubernetes Dashboard
	- `minikube dashboard`
	- `kubectl proxy`
		- authenticates with the API server on the master node
		- Makes the dashboard available on a different URL 
		- proxy port 8001

- Bearer Token
	- access token for client to connect to k8s API to access resources
	- token:
	`$ TOKEN=$(kubectl describe secret -n kube-system $(kubectl get secrets -n kube-system | grep default | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t' | tr -d " ")`
	- api server endpoint:
	`APISERVER=$(kubectl config view | grep https | cut -f 2- -d ":" | tr -d " ")`
	- access API server
	`curl $APISERVER --header "Authorization: Bearer $TOKEN" --insecure`



#kubernetes/edxIntroToKubernetes/chapter7	
#pivotal/flexhour