## what is pod ?








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
