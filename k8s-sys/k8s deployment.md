## what is k8s deployment ?


A k8s deployment provides a declarative way to define and manage the desired state of your application.

k8s deployment making it easier to handle updates and changes without manual intervention. 

A k8s eployment is a resource object in k8s that provides declarative updates for pods & replicasets.

They also provide features like auto-scaling and auto-healing to enhance the overall reliability and performance of your applications.

`Auto-Scaling` :-  When lots of people start using your app, Kubernetes can automatically create more copies of it to handle the extra traffic. This helps your app stay fast and responsive. 



`Auto-Healing` :- Sometimes parts of your app might stop working. Kubernetes notices this and replaces the broken parts with new ones automatically, so your app keeps running smoothly without you having to fix things manually.




### Key Concepts Of Kubernetes Deployment :- 


`Pods`  Think of pods as tiny packages for your apps. They can hold one or more containers. 

`ReplicaSets` ReplicaSets make sure you always have the right number of pod copies running. 

`Deployments` Imagine Deployments as managers for ReplicaSets.

`Scaling` With Deployments, you can make your app bigger or smaller by changing the number of copies. 

`Rolling Updates` If you want to change your app without causing downtime, Deployments help by slowly putting in new copies and taking out old ones.

`Rollbacks` If something goes wrong with an update, you can go back to the way things were before. 

`Health Checks` Kubernetes keeps an eye on your containers. It checks if they're ready to work (readiness) and if they're still doing their job. It's like a doctor making sure everyone's healthy and active.




### How to create k8s deployment file ?


##### step-1 :- create yaml file for deployment


```
vi mydeployment.yml
```


##### step-2 :- use below command for deployment
`


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mynginx-deployment
  labels:
    app: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: appcontainer
        image: nginx:latest
        ports:
        - containerPort: 80

```

`NB`

`apiVersion: apps/v1`  = specify the k8s api version and apps/v1 is the standard for eployments.

`kind: Deployment`  = type of k8s object

```
metadata:
  name: mynginx-deployment
  labels:
    app: myapp
```

metadata provides a name for the deployment and labels for identifying and grouping resources.

```
spec:
  replicas: 3
```
it specifies the desired no of pod replicas


```
selector:
    matchLabels:
      app: myapp
```
selector matches the pods with specified label


```
template:
    metadata:
      labels:
        app: myapp
```

the template defines the pod specification, including labels that match the selector


```
spec:
      containers:
      - name: appcontainer
        image: nginx:latest
        ports:
        - containerPort: 80
```

define the container inside each pod, name= here container name, image= docker container create image, ports= exposes port 80 inside the container



##### step-3 :- apply the deployment


```
kubectl apply -f mydeployment.yml
```


##### step-4 :- check the deployment


```
kubectl get deployments
```


##### step-5 :- check the pods status


```
kubectl get pods
```

OPTIONALS :-
==================


##### step-6 :- check the pods detailed info


```
kubectl describe pod <pod-name>
```


##### step-7 :- check logs from a pod


```
kubectl logs pod <pod-name>
```
