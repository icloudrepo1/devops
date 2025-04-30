## What is namespace ?


In Kubernetes (k8s), a Namespace is basically a way to divide cluster resources between multiple users or projects.

You can think of it like this :-

  - Imagine Kubernetes as a giant apartment building.
    
  - Each Namespace is like a separate apartment within that building.

  - Inside each apartment (Namespace), you can have your own furniture (Pods, Services, Deployments, etc.) without bothering the neighbors.
    
  - They’re isolated from each other, but still living in the same overall building (the cluster).
    
  - In one namespace, you can have App A  and In another namespace, you can have App B.


    
### Why use Namespaces ?


`Organization :-` Helps separate environments (like dev, staging, production).

`Resource limits :-` You can apply quotas to prevent one team from hogging all the cluster resources.

`Access control :-` You can set up rules so that different teams can only see or modify stuff in their own namespace.


#### note :- 

Kubernetes starts with some built-in namespaces like.

   - default :- Where stuff goes if you don’t specify a namespace.

   - kube-system :- Where k8s system stuff runs (like networking plugins, DNS, etc.).

   - kube-public :- Public stuff available to everyone (rarely used).




### Namespace Commands


1. List all namespaces

```
kubectl get namespaces
```

OR

```
kubectl get ns
```


2. Create a new namespace

```
kubectl create namespace <name>
```


3. Show details about a namespace

```
kubectl describe namespace <name>
```


4. Delete a namespace

```
kubectl delete namespace <name>
```


5. How to set/switch to namespace(default/custom) for your current kubectl session

```
kubectl config set-context --current --namespace=<name>
```

6. How to check what is your current namespace

```
kubectl config view --minify --output 'jsonpath={..namespace}'
```



=========END===========================
