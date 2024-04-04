# What is kubernetes?
_Kubernetes also known as "K8s", is an open-source container archestration platform developed by google._

_IT is designed to automate the deployment, scaling and manegemnt of containerized applications across cluster of nodes._

_Kubernetes provides a consistent and reliable way to manage applications, regardless of whether they are running on-premises, in the cloud or in the hybrid environments_

Nodes:
-------------
* A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine,
  depending on the cluster.
* Each Node is managed by the control plane
* A Node can have multiple pods, and the Kubernetes control plane automatically handles
  scheduling the pods across the Nodes in the cluster. 

Every Kubernetes Node runs at least:
* Kubelet, a process responsible for communication between the Kubernetes control plane and
  the Node. it manages the Pods and the containers running on a machine.
* A container runtime (like Docker) responsible for pulling the container image from a registry,
  unpacking the container, and running the application.

What is Kubernetes Cluster? 
* A Kubernetes cluster is a set of nodes that run containerized applications. 
* Containerized applications packages an app with its dependencies and some necessary services.
* Kubernetes clusters allow containers to run across multiple machines and environments:
  virtual, physical, cloud-based, and on-premises.

PODS:
===========
* Pods are the smallest, most basic deployable objects in Kubernetes.
* A Pod represents a single instance of a running process in your cluster.
* Pods contain one or more containers, such as Docker containers. 
* When a Pod runs multiple containers, the containers are managed as a single entity and 
  share the Pod's resources.

Kubernetes Features:
========================
1)Managing Multiple Containers as one entity
2)Resource Usage Monitoring
3)Health Checks
4)Networking
5)Load Balancing

========================================================================================

What is minikube?
* Minikube is a tool that makes it easy to run kubernetes locally.
* Minikube runs a single-node kubernetes cluster inside a vitual machine on your laptop
  for users looking to try out kubernetes

What is KUBECTL?
* kubectl is command line interface for running commands againist kubernetes clusters

* download chocolatey windows
  https://chocolatey.org/install
  chocolatey --version
  choco
  choco install minikube       : To install minikube
  choco install kubernetes-cli : To install kubectl
 
  systeminfo
  minikube start --driver=<driver-name>c
  minikube stop
  minikube status
  minikube dashboard
  minikube delete
  minikube docker-env

  kubectl cluster-info
  
  kubectl get node

  kubectl get deployment
  
  kubectl get replicaset
  
  kubectl get pod
 
  kubectl get service

  kubectl create deployment nginx-server --image=imageName  --port=<port-no>: To Create a deployment for given image
  
  kubectl expose deployment <deployment-name> --type=NodePort : To create service of type NodePort



  kubectl delete deployment deployment-name   : To Delete a deployment
  kubectl describe deployment deployment-name : To Describe a deployment
  kubectl describe pod pod-name : To Describe a pod
  kubectl edit deployment deployment-name  : To Edit A Deployment
  kubectl logs pod-name
  kubectl get nodes


  kubectl create namespace name_of_namespace
  kubectl get namespace
  kubectl delete namespace name_of_namespace
	
  kubectl -h 
  

  kubectl logs pod-name

  kubectl apply -f configuration_file_name.yml : create deployment in default namespace
  kubectl apply -f configuration_file_name.yml --namespace=<namespace-name> : create deployment
                                         in provided namespace
  kubectl get deployment --namespace=<namespace-name>
  kubectl get pod --namespace=<namespace-name>

  kubectl delete -f configuration_file_name.yml

  minikube service service_name --url: To Start a service

  kubectl get all


  kubectl exec -it <pod_name> bash

  https://amazon-eks.s3.us-west-2.amazonaws.com/cloudformation/2020-07-23/amazon-eks-vpc-private-subnets.yaml

  

  aws eks --region us-east-2 describe-cluster --name <cluster-name> --query cluster.status

  aws eks update-kubeconfig --region us-east-2 --name <cluster-name>
  
  aws sts get-caller-identity

  aws iam list-users

  Node Group Attach Below Policy to Role
  
  * AMAZONEKS_CNI_POLICY
  * AmazonEKSWorkerNodePolicy
  * AmazonEC2ContainerRegistryReadOnly

  kubectl get nodes --watch

  
  minikube addons list

  minikube tunnel





==========================================================================
==============================================================================
Deploy Spring Boot App With Kubernetes
=============================================================
1)minikube start
2)minikube status
3)kubectl create namespace rajdemo
4)Create manifest file which will be used for creating pods and services.
  >kubectl create deployment eureka-server-deployment --image=raj2244/sample-app-1:latest --dry-run -o=yaml > eurek-server-deployment.yaml
  >kubectl create service <service-type> <service-name> --tcp=8080:8080 --dry-run -o=yaml > eurek-server-service.yaml
5)Deployment file points to spring boot application image and it pull that image once Pod is
  being created.
  >kubectl create -f deployment.yaml  
  >kubectl create -f service.yaml  

6)minikube service <service-name>
*****************************************************************************

6)Make sure that everything is up and running .
  >kubectl get all -n rajdemo


7)Enable port forwarding for accessing Spring boot application
  >kubectl port-forward service/rajdemo 8080:8080 -n rajdemo


Access the MySQL Database inside the cluster
** kubectl exec -it <pod_name> bash

Then use the command below to connect to the MySQL server.
** mysql -u root -p 

