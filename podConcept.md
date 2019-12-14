# **PODS: **

> ## **Introduction**
The smallest, simplest and independent unit in the Kubernetes object model that you can create or deploy. In simple words a pod is a group of one or more containers. A Pod encapsulates an application's container. i.e. a pod can contain main application container and one or more supporting containers to support the main application. there can multiple pods running on one worker node. each pod will have it's own IP, storage resource. containers inside one pod are linked together and can communicate with each other with **localhost.** One point to note is that when we say a pod is running that actually means one or more containers  are running in a unique environment and that unique environment is referred as pod.
