## what is pod ?


Kubernetes doesn't manage containers directly—it manages pods. 

A Kubernetes (k8s) pod is the smallest and simplest unit in the Kubernetes object model that you can create or deploy and manage.

A pod is a wrapper around one or more containers (usually Docker containers) that are deployed together on the same host, share the same network and storage, and are treated as a single unit.

A pod can run a single container or multiple tightly coupled containers that share the same resources.

Pods are ephemeral. If a pod dies, Kubernetes can automatically create a new pod, but it will be a new instance with a different IP.

All containers in a pod share the same IP and port space.

Containers in a pod are started, stopped, and managed together.


### How to create pod inside default namespace ?


##### step-1 :- create yaml file for pod create


```bash
vi mypodcrt.yml
```


##### step-2 :- use below command for pod create


`A. If it is kubeadm then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  nodeSelector:
    kubernetes.io/hostname: worker-1
  containers:
    - name: container1
      image: nginx
      ports:
        - containerPort: 80

```


`B. If it is minikube then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
  - name: container1
    image: nginx
    ports:
    - containerPort: 80

```


##### step-3 :- apply the manifest file(mypodcrt.yml) to create the pod


```
kubectl apply -f mypodcrt.yml
```


##### step-4 :- verify the pod's status


```
kubectl get pods
```

##### step-5 :- to verify pod's detail info


```
kubectl get pod pod1 -o wide

```



### How to create pod inside custom namespace ?


##### step-1 :- List all namespaces and if no custom namespaces there , then you create a custom namespaces


A. verify all namespaces


```
kubectl get namespaces
```

OR

```
kubectl get ns
```


B. Create a new custom namespace


```
kubectl create namespace <name>
```


##### step-2 :- create yaml file for pod create


```bash
vi mypodcrt.yml
```


##### step-3 :- use below command for pod create


`A. If it is kubeadm then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  namespace: <namespacename>
spec:
  nodeSelector:
    kubernetes.io/hostname: worker-1
  containers:
    - name: container1
      image: nginx
      ports:
        - containerPort: 80

```


`B. If it is minikube then👇👇`


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  namespace: <namespacename>
spec:
  containers:
  - name: container1
    image: nginx
    ports:
    - containerPort: 80

```


##### step-4 :- apply the manifest file(mypodcrt.yml) to create the pod


```
kubectl apply -f mypodcrt.yml
```


##### step-5 :- verify the pod's status


```
kubectl get pods
```

##### step-6 :- to verify pod's detail info


```
kubectl get pod pod1 -o wide

```


=======END===========
