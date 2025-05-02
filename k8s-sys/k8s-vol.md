## what is k8s-volume ?


in k8s, when a container crashes or restarts, any data inside it is lost so volumes solve this by providing persistent or shared storage.

k8s volume is a storage resources that containers in a pod can use to store & share data.

unlike the ephemeral storage inside containers, a volume can persist data beyond the containers life.



### how to use k8s-volume ( multiple file = pv, pvc, podusepvc)


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


##### step-9 :- Use pvc in a pod


`vi mypvcuse.yml`


```
apiVersion: v1
kind: Pod
metadata:
  name: pvc-use-pod
spec:
  containers:
  - name: cont1
    image: nginx:latest
    command: [ "sh", "-c", "echo 'hii all i m ram' > /data/mydata.txt && sleep 3600" ]
    volumeMounts:
    - mountPath: /data
      name: my-datastorage
  volumes:
  - name: my-datastorage
    persistentVolumeClaim:
      claimName: my-pvc

```


##### step-10 :- apply pvc in a pod create file


```
kubectl apply -f mypvcuse.yml
```

##### step-11 :- verify pvc is mounted (inside pod)


```
kubectl get pod pvc-use-pod
```

##### step-12 :- go inside pod and check your data


```
kubectl exec -it pvc-use-pod -- sh
```

```
cat /data/mydata.txt
```

OR

```
cd data/
```

```
cat mydata.txt
```



### how to use k8s-volume ( single file)


##### step-1 :- create a file


`vi myk8svoluse.yml`


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

---

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

---

apiVersion: v1
kind: Pod
metadata:
  name: pvc-use-pod
spec:
  containers:
  - name: cont1
    image: nginx:latest
    command: [ "sh", "-c", "echo 'hii all i m ram' > /data/mydata.txt && sleep 3600" ]
    volumeMounts:
    - mountPath: /data
      name: my-datastorage
  volumes:
  - name: my-datastorage
    persistentVolumeClaim:
      claimName: my-pvc

```


##### step-2 :- apply it


```
kubectl apply -f myk8svoluse.yml
```


##### step-3 :- check your pod status


```
kubectl get pod pvc-use-pod
```


##### step-4 :- go inside pod and check your data


```
kubectl exec -it pvc-use-pod -- sh
```

```
cat /data/mydata.txt
```

OR

```
cd data/
```

```
cat mydata.txt
```



### how to delete k8s-volume


##### step-1 :- delete the pod first


```
kubectl delete pod pvc-use-pod
```

```
kubectl get pod
```

##### step-2 :- delete the pvc


```
kubectl delete pvc my-pvc
```

```
kubectl get pvc
```

##### step-3 :- delete the pv now


```
kubectl delete pv my-pv
```

```
kubectl get pv
```


=========END=============
