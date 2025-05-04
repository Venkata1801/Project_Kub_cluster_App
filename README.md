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



         
         










