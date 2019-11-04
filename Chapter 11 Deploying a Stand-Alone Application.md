# Chapter 11 Deploying a Stand-Alone Application
`minikube start`
`minikube status`
`minikube dashboard`


### Creating an App on dashboard

“+ Create”
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.40.58%20PM.png)
“Deploy”
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.41.45%20PM.png)
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.41.57%20PM.png)
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.42.05%20PM.png)
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.42.32%20PM.png) kubectl describe pod <pod_id>

### List Pods with Labels
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.54.06%20PM.png)
![](Chapter%2011%20Deploying%20a%20Stand-Alone%20Application/Screen%20Shot%202019-08-30%20at%202.57.15%20PM.png)

### Delete deployment
`kubectl delete deployments webserver`
	- Deletes the ReplicaSet and Pods

### Deploy an App Using the CLI
Create `webserver.yaml` with:
```
apiVersion: apps/v1 kind: Deployment metadata: 	name: webserver 	labels: 		app: nginx spec: 	replicas: 3 	selector: 		matchLabels: 			app: nginx 	template: 		metadata: 			labels: 				app: nginx 		spec: 			containers: 			- name: nginx 			  image: nginx:alpine 			  ports: 			  - containerPort: 80
```

`kubectl create -f web server.yaml`

### Exposing an App
Create a `webserver-svc.yaml` with:
```
apiVersion: v1 kind: Service metadata:   name: web-service   labels:     run: web-service spec:   type: NodePort   ports:   - port: 80     protocol: TCP   selector:     app: nginx
```

Create the Service:
`kubectl create -f web server-svc.yaml`

Exposing a Deployment with the `kubectl expose` command:
`kubectl expose deployment webserver --name=web-service --type=NodePort service/web-service exposed`