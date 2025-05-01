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
  name: reddit-clone-deployment
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

apiVersion and kind tell Kubernetes that is a Deployment.

metadata includes the name "reddit-clone-deployment" and labels to identify the app as "reddit-clone". 

spec.replicas  says we want 3 copies (replicas) of our app running.

spec.selector  helps the ReplicaSet know which Pods to manage.

matchLabels  says to find Pods with the label " app: reddit-clone ".

spec.template  defines how the Pods look. 

metadata.labels  sets the label " app: reddit-clone " for the Pods.

spec.containers  lists what runs inside each Pod.

name  is " reddit-clone " for the container.

image  specifies the container image to use.

ports  tell's Kubernetes that the app inside the container listens on port 8000.




##### step-3 :- apply the deployment


```
kubectl apply -f mydeployment.yml
```


