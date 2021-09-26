
   elk:
   https://youtu.be/ykuw1piMGa4?t=289
   
   
   es cluster spread to different machines with docker
   https://xyzcoder.github.io/2020/07/22/how-to-deploy-an-elastic-search-cluster-consisting-of-multiple-hosts-using-es-docker-image.html
   
   
   my wifi driver:
   killer wifi 6 ax500-dbs
   
   
$ kubectl describe pods 
Name:         kubernetes-bootcamp-fb5c67579-jgh9m
Namespace:    default
Priority:     0
Node:         minikube/172.17.0.22
Start Time:   Sat, 18 Sep 2021 12:40:22 +0000
Labels:       app=kubernetes-bootcamp
              pod-template-hash=fb5c67579
Annotations:  <none>
Status:       Running
IP:           172.18.0.3
IPs:
  IP:           172.18.0.3
Controlled By:  ReplicaSet/kubernetes-bootcamp-fb5c67579
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://99cde78228446fac5e7c4666218d2aeccab41a9fc94dc05265a0fe6378a1fc67
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Sat, 18 Sep 2021 12:40:24 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-rqzpw (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  default-token-rqzpw:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-rqzpw
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                 node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  83s   default-scheduler  Successfully assigned default/kubernetes-bootcamp-fb5c67579-jgh9m to minikube
  Normal  Pulled     82s   kubelet            Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal  Created    82s   kubelet            Created container kubernetes-bootcamp
  Normal  Started    81s   kubelet            Started container kubernetes-bootcamp
  
  
  
  each Pod in a Kubernetes cluster has a unique IP address, even Pods on the same Node
  
  
  Services have an integrated load-balancer that will distribute network traffic to all Pods of an exposed Deployment. 
  
  To list your deployments use the get deployments command: 
  `kubectl get deployments`
  
  To see the ReplicaSet created by the Deployment, run 
  kubectl get rs
  
  execute command inside a pod
  kubectl exec -ti $POD_NAME -- curl localhost:8080
  
  
  
  export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
  echo NODE_PORT=$NODE_PORT
  
  curl $(minikube ip):$NODE_PORT
  
  
  create a new service and expose it to external traffic we’ll use the expose command with NodePort as parameter
  (minikube does not support the LoadBalancer option yet):

  kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
  
  
  In the previous module we scaled our application to run multiple instances. This is a requirement for performing updates without affecting application availability. By default, the maximum number of Pods that can be unavailable during the update and the maximum number of new Pods that can be created, is one.