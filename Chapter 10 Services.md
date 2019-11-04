# Chapter 10 Services
## Connecting Users to Pods
![](Chapter%2010%20Services/Screen%20Shot%202019-08-23%20at%2011.54.10%20AM.png) User is connected to a Pod via its IP address
![](Chapter%2010%20Services/Screen%20Shot%202019-08-23%20at%2011.54.29%20AM.png) VM terminates, new one gets spun up using different IP address, user cannot connect

K8s provides a higher-level abstraction `Service`
	- logically groups Pods and defines a policy to access them via `Labels` and `Selectors`


## Services
![](Chapter%2010%20Services/Screen%20Shot%202019-08-23%20at%2012.05.45%20PM.png)
Using `Selectors` 
	- `app==frontend`: 3 pods
	- `app==db`: 1 pod

`Service` is used to assign a name to the logical grouping
	- Service `frontend-svc` names the Selector `app==frontend`

`app` is the Label key
`frontend` and `db` are Label values

![](Chapter%2010%20Services/Screen%20Shot%202019-08-23%20at%202.16.43%20PM.png) 
`frontend-svc` Service for all Pods with Label key `app` and value `frontend`


![](Chapter%2010%20Services/Screen%20Shot%202019-08-23%20at%206.16.40%20PM.png)
Each Service gets a ClusterIP (routable only inside the cluster)

Service receives requests on port 80
Pods receive requests using targetPort 5000 by default

Service endpoint: logical set of a Pod’s IP address w/ targetPort

Endpoints are created and managed automatically by the Service, not the K8s cluster admin.


## Kube-Proxy
API watcher on every worker node
Watches for addition/removal of Services and endpoints
![](Chapter%2010%20Services/Screen%20Shot%202019-08-23%20at%206.31.21%20PM.png)
kube-proxy configures iptables rules to capture the traffic for its ClusterIP and forwards it to one of the Service's endpoints

Receive external traffic, route it internally inside the cluster based on the iptables rules

When Service is removed, kube-proxy removes the corresponding iptables rules on all nodes as well


## Service Discovery
When a Pod starts on a worker node, the kubelet daemon sets env vars in the Pod for all active Services

![](Chapter%2010%20Services/Screen%20Shot%202019-08-25%20at%2012.33.20%20PM.png)
env vars for active Service `redis-master` that exposes `port 6379` with ClusterIP `172.17.0.6`
Note: if Service is created after Pods, they won't have env vars.

	- DNS
		- add-on that creates a DNS record for each Service
		- `my-svc.my-namespace.svc.cluster.local`
		- Services within that namespace can find each other by the name all Pods in namespace `my-ns` can look up `redis-master`
		- Pods in other NS can look up `redis-master.my-ns`


## ServiceType
Defines accessibility scope
	- cluster
	- cluster + external
	- maps to an entity (inside or outside of cluster)

ClusterIP (default)
	- Service receives a Virtual IP address for communication
	- only accessible within the cluster

NodePort
![](Chapter%2010%20Services/Screen%20Shot%202019-08-25%20at%203.03.59%20PM.png)
	- In addition to a ClusterIP
	- port dynamically picked from default range of 30000-23767
	- mapped to the Service
	- NodePort `32233` for Service `frontend-svc`
		- All traffic would be redirected to assigned ClusterIP `172.17.0.4`
	- Easy to access externally

LoadBalancer
![](Chapter%2010%20Services/Screen%20Shot%202019-08-25%20at%204.10.53%20PM.png)
	- NodePort & ClusterIP are automatically created
		- external LB will route to them
	- Service is exposed at a static port (NodePort) on each worker node
	- Only work if the infrastructure supports auto-creation of LB for K8s

ExternalIP
![](Chapter%2010%20Services/Screen%20Shot%202019-08-25%20at%204.33.45%20PM.png) 
	- A Service is mapped to an ExternalIP address if it can route to 1+ worker nodes
	- Ingressed traffic via ExternalIP gets routed to one of the Service endpoints
	- Not managed by K8s

ExternalName
	- no Selectors and doesn't define any endpoints
	- returns a `CNAME` record of an externally configured Service
	- allows externally configured Services (database, etc.) available to apps inside the cluster
	- apps can access the service by the name in the same namespace


#kubernetes/edxIntroToKubernetes/chapter10	
#pivotal/flexhour