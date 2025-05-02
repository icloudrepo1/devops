## what is k8s-volume ?


in k8s, when a container crashes or restarts, any data inside it is lost so volumes solve this by providing persistent or shared storage.

k8s volume is a storage resources that containers in a pod can use to store & share data.

unlike the ephemeral storage inside containers, a volume can persist data beyond the containers life.
