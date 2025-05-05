## what is ConfigMap


In Kubernetes, a ConfigMap is a resource object that allows you to store configuration data separately from your application code. 

In Kubernetes (k8s), ConfigMaps are API objects used to store non-confidential configuration data in key-value pairs.

It is a key-value store where you can store configuration settings, environment variables, or any other configuration-related data that your application needs. 

ConfigMaps are typically used to decouple configuration from application code, making it easier to manage and update configurations without changing the code itself.

ConfigMaps are often used to store configuration files in a key-value format, such as INI files, JSON, or YAML. 

When you create a ConfigMap, you specify the configuration data as key-value pairs. This data can then be mounted as volumes in your pods or injected into container environments as environment variables.

They act as a centralized repository for configuration settings that can be used by various components inside your stack.

`EXAMPLE `

Imagine you're in charge of a big spaceship (Kubernetes cluster) with lots of different parts (containers) that need information to function properly. 

ConfigMaps are like a file cabinet where you store all the information each part needs in simple, labeled folders (key-value pairs).



## Web-App hosting using configmap



### Step 1 :- Create combined YAML file


`vi mywebapp-complete.yml`


```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-web-content-configmap
  namespace: default
data:
  index.html: |
    <!DOCTYPE html>
    <html>
    <head>
      <title>My WebApp-2025</title>
    </head>
    <body>
      <h1>Welcome to Kubernetes session!</h1>
      <h1>configmap</h1>
    </body>
    </html>
---
apiVersion: v1
kind: Pod
metadata:
  name: my-webapp
  namespace: default
  labels:
    app: my-webapp
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
    volumeMounts:
    - name: web-content
      mountPath: /usr/share/nginx/html
      readOnly: true
  volumes:
  - name: web-content
    configMap:
      name: my-web-content-configmap
---
apiVersion: v1
kind: Service
metadata:
  name: my-webapp-service
  namespace: default
spec:
  type: NodePort
  selector:
    app: my-webapp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30081


```

### Step 2 :- Apply it

```
kubectl apply -f mywebapp-complete.yml
```

##### `NB`

`Why You Need a Service ?`

Kubernetes Pods are ephemeral and their IPs change frequently. So, directly accessing a Pod by its IP is unreliable.

A Service :-

 - Acts as a stable endpoint (a permanent IP or DNS name).
 - Load balances traffic to all matching Pods.
 - Enables network communication inside the cluster (or from outside, depending on the service type).



