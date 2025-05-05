## what is ConfigMaps


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
