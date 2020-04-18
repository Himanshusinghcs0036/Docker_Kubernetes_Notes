#### RUN A Deployment from command line <br />
> kubectl run deploymentName --image imageName --replicas replicacount <br />
  Example:
  
### Exposing a Port </br >
> </br >
 > 1. kubectl expose deployment nginx --type NodePort --port 8080 </br >
>   <br>
 > 2. kubectl expose replicaset.apps/nginx-79d79754b6 --port=8084 --target-port=8084 --name=ngnix-service --type=LoadBalancer </br >
  
