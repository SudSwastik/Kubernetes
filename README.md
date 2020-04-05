### Installation(MacOS)

- To Run Kubernetes in Local Operating System:

> install a Hypervisor such as VirtualBox

>Install Minikube:  
Minikube is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a Virtual Machine (VM) on your laptop for users looking to try out Kubernetes or develop with it day-to-day.
```shell
$ brew install minikube
```

> Start Minikube

```shell
$ minikube start
```
> Confirm Installation

```shell
$ minikube status
```

# Pods

>A Pod is the basic execution unit of a Kubernetes application–the smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents processes running on your Cluster.


 >Manual Pod Creation
- Creates a Pod along with it a Deployment and replicaset is also created

 ```
 $ kubectl run my-nginx --image=nginx:alpine
 ```

> To List Everyting 

```
$ Kubectl get all
```

> To Delete Pod 
- Get PodName From get all or get pods command
- It deletes pod but again it regenerate pod. So, to completely delete the pod we have to delete the deployment
```
$ Kubectl delete pod <Pod-Name>
```

> To Access Pod 
- Get PodName From get all or get pods command
- Pass PodName and external Port:Pod internal Port

```
$ kubectl port-forward my-nginx-576bb7cb54-5rbc8 9090:80
```

>To completely delete Pod
- Name of Pod Deployment

```
$ kubectl delete deployment my-nginx
```

>Create  Pod Through Yml File
- Creates a Pod along with No replicaset and deployment

 ```
 $ kubectl create -f  Pods/nginx.pod.yml
 ```

 >View Full Pod Properties
 ```
 $ kubectl describe pod <Pod-Name>
 ```

 >Modify Changes and update pod
 - It updates the Pod. If not created, Creates a new Pod
 ```
 $ kubectl apply -f <Pod-FileName>
 ```

 >To Go inside Container
 ```
 $ kubectl exec my-nginx -it sh
 ```

 >To Delete Pod
 ```
 $ kubectl delete -f <Pod-FileName>
 ```

 >To edit Yml Files
 ```
 $ kubectl edit -f <Pod-FileName>
```
 # Pod Liveness and Readiness Check

 - It Checks If the Container is working and When it is ready for interaction  

 ```
 $ 
    livenessProbe:
      httpGet:
        path: /index.html
        port: 80
      initialDelaySeconds: 15
      timeoutSeconds: 2 # Default is 1
      periodSeconds: 5 # Default is 10
      failureThreshold: 1 # Default is 3
    readinessProbe:
      httpGet:
        path: /index.html
        port: 80
      initialDelaySeconds: 3
      periodSeconds: 5 # Default is 10
      failureThreshold: 1 # Default is 3
 
 ```

 # Deployment

 > A Deployment provides declarative updates for Pods and ReplicaSets.


 >To Create Deployment
 ```
 $ kubectl apply -f nginx.depoyment.yml
```

>To List All Pods

```
 $ kubectl get pods
```

>To List All Pods with a Specific Label
- L stands for Label Selector Followed by key:value pair of selector
```
$ kubectl get pods -l app=nginx
```

> To Create Deployment From Local images
- Run docker compose to create 3 images

```
$ docker-compose build
```

- Create service to talk to pod

```
$ kubectl apply -f node-app.node-app.service.yml
```

>To create Deployment
- Creates pod based on yml files
- When second or third Deploment yml is run. It terminates the first  or second yml pod as both have same  Name
```
$ kubectl apply -f node-app-v1.deployment.yml
```

> To test output
- service created is of type LoadBalancer whose external ip is by default localhost
- Prints the response by node server
```
$ localhost
```


# Service
> A Service provides a single point of entry for accessing one or more pods

- There are 4 types of services 
1. ClusterIp - Used to Connect Different pod internally
2. NodePort - Used to asssign a custom to talk to port
3. LoadBalancer - Acts as a loadbalancer between different pods
4. ExternalIp

> Craete a Cluster service
```
$ kubectl apply -f Services/clusterIp.service.yml
```

# Volumes

>It is used for Sharing/persisting data From Pod

- To create an Empty Volume
```
$ kubectl apply -f Volumes/nginx-alpine-emptydir.pod.yml
```

