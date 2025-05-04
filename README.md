# Project Name :Kubernetes Vote application 
This project demonstrates hoe to deploy a microservices-based Voting application using kubernetes. This application allows user to between two options example cats vs dogs.

# Deployment of the Kubernetes Cluster
Step 1 : Login to the GCP Via - https://console.cloud.google.com/kubernetes/
Step 2 : Go to Menu -> click on Kubernetes Engine -> clusters -> click on " Create" which will create a new K8s cluster
Step 3 : switch to Standard cluster
Step 4 : Name : CLuster 1 , Zone - select which one is near to you. I have selected "us-central1-c"
Step 5 : only one change need to do is go to default- pool -> Node -> Image type -> change it to "Ubunutu with containerd" . Ubunutu will be the operating system for the work nodes and container D will be the run time. back to cluster basics
Step 6 : Press Create
Step 7 : wait for 6 to 8 min and the cluster will be created.
Step 8 : CLick on the cluster name and you can see the details, Nodes, Storage, Observability and logs.
Step 9 : click on nodes and deom there you can see Three worker nodes have been created They are basically VMs on google cloud platform and act as worker nodes for the kubernetes cluster.
Step 10: if you click on logs you can see the logs if in case if there are any issues in the cluster to idenify.
Step 11 : if you go back to Overview of the cluster it will provide brief information about Nodes Virtual CPU's and Total Memory of the cluster etc.
Step 12 : for documenation and cheat sheet the following URL are important for all Engineers
         Kubernetes Documentation | Kubernetes - https://kubernetes.io/docs
         cheat sheet for CLI : https://kubernetes.io/docs/reference/kubectl/quick-reference/
# Activate Cloud shell machine on Kubernetes cluster
Cloudshell is actually a terminal environment for the google cloud.
Step 1 : Menu -> Compute Engine -> VM instances -> Click on right hand top >- icon 
Step 2 : A black window will open. Cloudshell is a google cloud terminal machine to perform any google cloud operation on kubernetes cluster or any compute enginer or any other google cloud machine.
Step 3: It will check for authorization and then your username and project name will be Visible.
Step 4 : Type-  kubectl get nodes
NAME                                       STATUS   ROLES    AGE     VERSION
gke-cluster-2-default-pool-7889c4a5-gvdq   Ready    <none>   4d22h   v1.32.2-gke.1182003
gke-cluster-2-default-pool-7889c4a5-t7qm   Ready    <none>   4d22h   v1.32.2-gke.1182003
gke-cluster-2-default-pool-7889c4a5-x0qt   Ready    <none>   4d22h   v1.32.2-gke.1182003

Step 5 : Type- kubectl get nodes -o wide . it will provide more fields with internal and external ip's, Obuntu OS , Kernel information and Contianer runtime that is containerD information etc.
# Cluster structure
A typical cluster Structure includes the following components 
1. Kubernetes components of Control plane (Masternode) which is managed by GCP - API server, Scheduler, Controller Manager and etcd
2. Kubernetes components of the Worker node - Nodes ( Virtual machines), Kubelet , Kubeproxy, pods, contianers  and contianer runtime.
3. Image store Registry : the container runtime will pull contianer images from the register.

# Sample voting application deployment on kubernetes ( reference : https://github.com/gsm-asad/example-voting-app)
Application by which you can vote on cats versus dogs ona  weblink and you can check the result of the voting ( Percentage of votes for cats and dogs). It has two Microservices on is the voting service and other one is result service.
# Application components
1. An application with two user interfaces ( UI) - Voting app (Webink) and result app (Weblink)
2. Two Databases,  Redis and PostgreSQL.
3. Work Module which is for Data processing ( Assume the developers already built the code for the application and images are uploaded it inthe registry).
4. All the user facing pods are webservers ( Voting app and result app) are listening on port 80
5. Redis DB pod is listening the web traffic from vote app on port 6379
6. PostgreSQl pod is listening on port 5432
7. pods will be deployed ussing deployments
8. links between pods will be established using kuberentes services
9.  5 deployments (Pods) - Voting, result , redis, postgresql db and worker module.
10. 4 services - Vote service (LB), result service (LB), redis service ( Cluster IP) and db-service (Cluster IP).

# Note : I have forked the directory from https://github.com/gsm-asad/example-voting-app and downloaded the K8s- Specifications. In specifications folder there are 9 YAML files ( 5 deployments and 4 services).
# Deployment 
Step 1 : uploaded K8s-Specifications folder
Step 2 : Verification by using the command 
drwxr-xr-x 2 pasupuleti_venkata               1001 4096 May  1 18:39 k8s-specifications
pasupuleti_venkata@cloudshell:~$ cd  k8s-specifications
pasupuleti_venkata@cloudshell:~/k8s-specifications$ ls -lrt
total 36
-rw-r--r-- 1 pasupuleti_venkata 1001 495 May  1 18:39 db-deployment.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 209 May  1 18:39 db-service.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 365 May  1 18:39 redis-deployment.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 221 May  1 18:39 redis-service.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 397 May  1 18:39 result-deployment.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 222 May  1 18:39 result-service.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 383 May  1 18:39 vote-deployment.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 214 May  1 18:39 vote-service.yaml
-rw-r--r-- 1 pasupuleti_venkata 1001 331 May  1 18:39 worker-deployment.yaml
Step 3: create Namespace vote 
pasupuleti_venkata@cloudshell:~/k8s-specifications$ kubectl get ns
NAME                          STATUS   AGE
default                       Active   5d1h
gke-managed-cim               Active   5d1h
gke-managed-system            Active   5d1h
gke-managed-volumepopulator   Active   5d1h
gmp-public                    Active   5d1h
gmp-system                    Active   5d1h
kube-node-lease               Active   5d1h
kube-public                   Active   5d1h
kube-system                   Active   5d1h
vote                          Active   3d2h
Step 4: check the componnets in the vote by creating Kubectl create -f k8s-specifications 
Pods:
pasupuleti_venkata@cloudshell:~/k8s-specifications$ kubectl get all -n vote
NAME                          READY   STATUS    RESTARTS   AGE
pod/db-5f694df55-7jjhx        1/1     Running   0          3d2h
pod/redis-56c45778b9-5qdlb    1/1     Running   0          3d2h
pod/result-775cdf58c8-pv4gj   1/1     Running   0          3d2h
pod/vote-b848587db-kwz9h      1/1     Running   0          3d2h
pod/worker-6cc4bdc555-w9s4q   1/1     Running   0          3d2h
Services:
NAME             TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)          AGE
service/db       ClusterIP      x.x.x.x   <none>               5432/TCP              3d2h
service/redis    ClusterIP      x.x.x.x    <none>              6379/TCP             3d2h
service/result   LoadBalancer   x.x.x.x    x.x.x.x             5001:31864/TCP     3d2h
service/vote     LoadBalancer   xx.xx.xx.xx   xx.xx.xx.xx    5000:32451/TCP   3d2h
Deployments:
NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/db       1/1     1            1           3d2h
deployment.apps/redis    1/1     1            1           3d2h
deployment.apps/result   1/1     1            1           3d2h
deployment.apps/vote     1/1     1            1           3d2h
deployment.apps/worker   1/1     1            1           3d2h
Replicas:
NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/db-5f694df55        1         1         1       3d2h
replicaset.apps/redis-56c45778b9    1         1         1       3d2h
replicaset.apps/result-775cdf58c8   1         1         1       3d2h
replicaset.apps/vote-b848587db      1         1         1       3d2h
replicaset.apps/worker-6cc4bdc555   1         1         1       3d2h
Pods in the vote namespace:
pasupuleti_venkata@cloudshell:~/k8s-specifications$ kubectl get pods -n vote
NAME                      READY   STATUS    RESTARTS   AGE
db-5f694df55-7jjhx        1/1     Running   0          3d2h
redis-56c45778b9-5qdlb    1/1     Running   0          3d2h
result-775cdf58c8-pv4gj   1/1     Running   0          3d2h
vote-b848587db-kwz9h      1/1     Running   0          3d2h
worker-6cc4bdc555-w9s4q   1/1     Running   0          3d2h
Services in the vote namespace
pasupuleti_venkata@cloudshell:~/k8s-specifications$ kubectl get svc -n vote
NAME     TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)          AGE
db       ClusterIP      XX.XXX.XXX.240   <none>           5432/TCP         3d2h
redis    ClusterIP      XX.XXX.XXX.XX    <none>           6379/TCP         3d2h
result   LoadBalancer   XX.XXX.XXX.97    XXX.XXX.XX.XXX   5001:31864/TCP   3d2h
vote     LoadBalancer   XX.XXX.XXX.99    XX.XX.XXX.XXX    5000:32451/TCP   3d2h
# Application has been deployed perfectly
# check by loggin into the load balancer ip address 
Step 1 : Go Kuberentes Engine -> Gateways,services & Ingress -> Select Services -> you can see result and vote with web url.
Step 2 : click on url ip of the vote : vote for dogs and click on url ip of th result -> Dogs 100% that means the application is working fine.
Step 3 : to check in another browser and click on vote for dogs or cat and check the results.

# Monitoring 
Step 1 : Go the Menu -> Monitoring -> Dashboards -> click on GKE .
Step 2 : From dashboard we can monitor Nodes, name spcaes, workloads, k8s services, pods, containers Status




         
         










