# ***STARTING WITH KUBERNETES***
![](https://github.com/Himanshusinghcs0036/Docker_Kubernetes_Notes/blob/master/KubeImages/K8Logo.png)

## *what is KUBERNETES: *
> Kubernetes is Container Orchestration Engine.
Container Orchestration job is to manage the Containers, services such as deployments, pods etc.
Kubernetes is often referenced with K8s that represents K for Start and s for end 8 character in between.
>>**Feature:**
1. Service discovery and load balancing
2. Storage orchestration
3. Automated rollouts and rollbacks
4. Automatic bin packing (Run containerized task with defined configuration)
5. Self-healing
5. Secret and configuration management

## *KUBERNETES Architecture: *

> Kubernetes follows master-slave architecture. Kubernetes supports one or master and can manage up to 5000 worker nodes.
![](https://github.com/Himanshusinghcs0036/Docker_Kubernetes_Notes/blob/master/KubeImages/MasterWorkerArchitecture.jpeg)

> ### **Master:**
![](https://github.com/Himanshusinghcs0036/Docker_Kubernetes_Notes/blob/master/KubeImages/K8Component.png)
Master refers to the process managing the cluster. Typically all these processes run on a single node in the cluster, and this node is also referred to as the master. The Kubernetes master is responsible for maintaining the desired state for your cluster.
All user requests goes through Master and Master decide/ manage how these requests will be served.
>> #### **Master Components:**
Master process can be divided into 4 components.
**1. etcd : ** Etcd is a light-weight key-value database. Kubernetes use etcd database to store current state of kubernetes cluster and also store the service configuration. Each kubernetes service query the etcd database (through API Server) to get the service state and any other required configuration information.
**2. API Server : ** API server is the gateway to Kubernetes cluster. Each service request will go through API server. User can connect to API server with *Kubectl* command or through UI.
That means, whenever a user communicate with Kubernetes cluster with Kubectl command, he/she actually communicate with API Server.
Other than this Object running on cluster connect to API server to modify the state of Object. the API server have *.rev* property (for server), indicating the snapshot in time and object has a *.mod* property (for object) indicating snapshot in time the object was last modified. By default these snapshot will be discarded in 5 minute.
*NOTE: Examples of Kubernetes Objects are Pod Objects, ReplicaSet Objects, and Deployment Objects.
**3. Scheduler :** As the name represents, scheduler schedules the services as per the defined configuration. As soon as user request for a service/ object to API server, API server update the etcd database with the service/object configuration. etcd database then notify the scheduler with the request. The scheduler create the service/POD as per the user defined configuration such as node, resource required.
**3. Controller Manager :** Process that runs controllers to handle Cluster background tasks. Basically the Controller watches the state of cluster through API server and when it gets notified, it make necessary change in order to take the cluster or service from current state to desired state. Controller are responsible for managing the health of pods, replication of pods and many other task to keep the objects in healthy state.

> ### **Worker / Node:**
A Worker Node is also referred to as a Node for short. A Node is an abstraction for a machine — either a physical machine or a virtual machine. Think of a Node as a computer server. Runs the Kubernetes agent that is responsible for running Pod containers via Docker or rkt, requests secrets or configurations, mounts required Pod volumes, does health checks and reports the status of Pods and the node to the rest of the system.
![](https://github.com/Himanshusinghcs0036/Docker_Kubernetes_Notes/blob/master/KubeImages/worker.png)
>> #### **Node Components:**
 Kubernetes worker can be divided into 3 components. these components run on each node.

 **1. container RunTime :** Downloads images and runs containers. For example, Docker is a Container Runtime.

 **2. Kubelet :** Kubelet is most important component of worker/ Node. It is kublet's task to run the pod and ensure that pod it in running state (As long it should be). It monitor the health of the running pod and keep the master updated with the pod state.
API Server invokes the Kubelet in the corresponding node to create the pod. kubelet talks to the container runtime  using the API over the Docker socket to create the container and then Kubelet updates the pod status to the API Server.

 **3. Kube-proxy :** Routes connections to the correct Pods. Also performs load balancing across Pods for a Service. Think traffic cop. It ensure that one node can talk with another node, one pod can communicate with other pod, one container can communicate with other container.


> ### ** Process Flow : **
![](https://github.com/Himanshusinghcs0036/Docker_Kubernetes_Notes/blob/master/KubeImages/MasterComponents.png)
*1.* kubectl writes to the API Server.
*3.* etcd notifies back the API Server.
*4.* API Server invokes the Scheduler.
*5.* Scheduler decides where to run the pod on and return that to the API Server.
*6.* API Server persists it to etcd.
*7.* etcd notifies back the API Server.
*8.* API Server invokes the Kubelet in the corresponding node.
*9.* Kubelet talks to the Docker daemon using the API over the Docker socket to create the container.
*10.* Kubelet updates the pod status to the API Server.
*11.* API Server persists the new state in etcd.


>> >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>************************************************************
