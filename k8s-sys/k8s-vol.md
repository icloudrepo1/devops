## what is k8s-volume ?


in k8s, when a container crashes or restarts, any data inside it is lost so volumes solve this by providing persistent or shared storage.

k8s volume is a storage resources that containers in a pod can use to store & share data.

unlike the ephemeral storage inside containers, a volume can persist data beyond the containers life.



### how to use k8s-volume ?


##### step-1 :- create a persistent volume(pv)


`vi ourpv.yml`


```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
  persistentVolumeReclaimPolicy: Retain

```


##### step-2 :- apply persistent volume(pv)


```
kubectl apply -f ourpv.yml
```

##### step-3 :- check persistent volume(pv) status


```
kubectl get pv
```

##### step-4 :- check persistent volume(pv) detailed info


```
kubectl describe pv my-pv
```

##### step-5 :- create a persistent volume claim(pvc)


`vi ourpvc.yml`


```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests: 
      storage: 300Mi

```


##### step-6 :- apply persistent volume claim(pvc)


```
kubectl apply -f ourpvc.yml
```


##### step-7 :- check persistent volume claim(pvc) status


```
kubectl get pvc
```


##### step-8 :- check persistent volume claim(pvc) detailed info


```
kubectl describe pvc my-pvc
```
