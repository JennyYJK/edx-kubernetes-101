# Chapter 14 Ingress
> An Ingress is a collection of rules that allow inbound connections to reach the cluster Services  

	- Abstraction deployed in front of the Service API resources
	- Offers a unified method of managing access to our applications from the external world
	- Centralize the routing rules management

	- Configures a Layer 7 HTTP/HTTPS load balancer for Services and provides:
		- TLS
		- Name-based virtual hosting
		- Fanout routing
		- Load balancing
		- Custom rules

![](Chapter%2014%20Ingress/Screen%20Shot%202019-09-02%20at%206.53.11%20PM.png)

	- Users don't directly connect to a Service
	- Users reach the Ingress endpoint
		- Request gets forwarded to the desired Service

``` name_based_virtual_hosting_ingress.yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: virtual-host-ingress
  namespace: default
spec:
  rules:
  - host: blue.example.com
    http:
      paths:
      - backend:
          serviceName: webserver-blue-svc
          servicePort: 80
  - host: green.example.com
    http:
      paths:
      - backend:
          serviceName: webserver-green-svc
          servicePort: 80
```
	- User requests to both `blue.example.com` and `green.example.com` would go to the same Ingress endpoint
	- Forwarded to `webserver-blue-svc` and `webserver-green-svc`

``` fanout_ingress.yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: fan-out-ingress
  namespace: default
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /blue
        backend:
          serviceName: webserver-blue-svc
          servicePort: 80
      - path: /green
        backend:
          serviceName: webserver-green-svc
          servicePort: 80
```
	- Requests to `example.com/blue` and `example.com/green` would be forwarded to `webserver-blue-svc` and `webserver-green-svc`

![](Chapter%2014%20Ingress/Screen%20Shot%202019-09-02%20at%206.59.12%20PM.png) fan out ingress vs virtual hosting ingress


## Ingress Controller
	- Watches the Master Node's API server for changes in the Ingress resources
	- Updates the Layer 7 Load Balancer

`minikube addons enable ingress`
`kubectl create -f name_based_virtual_hosting_ingress.yaml`
	- creates an Ingress resource using Ingress rule definition in file

![](Chapter%2014%20Ingress/Screen%20Shot%202019-09-02%20at%209.07.36%20PM.png)



#pivotal