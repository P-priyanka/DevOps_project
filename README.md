# DevOps_project
AWS EKS High-Availability Deployment for Interdependent Applications

# Description
This GitHub project focuses on deploying two interdependent application components, A and B, acquired from a third-party vendor, in an AWS Elastic Kubernetes Service (EKS) environment. The goal is to ensure high availability and optimal performance while adhering to the company's "container-first" philosophy.

# Pre-requisites
1. Make a cluster in EKS
2. Within cluster make Node Group which will create 3 instances in different availability zones, according to the subnet we chose while creating the Cluster
3. In these instances we will deploy our App A and App B
4. Install kubectl in cloudshell
   
`curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"`

`chmod +x kubectl`

`sudo mv kubectl /usr/local/bin`

To check if it is installed successfully.

`kubectl version`

# Create Deployments

`kubectl apply -f deploymentA.yaml`
`kubectl apply -f deploymentB.yaml`

# Checks node 

`kubectl get nodes`

# TO CHECK EACH NODE CONTAINS 2 APP(Change nodename from the above kubectl get node command)

`kubectl get pods --field-selector spec.nodeName=NODENAME`

# check pods
`kubectl get pod

# TO SEE ALL THE DEPLOYMENT RUNNING ON DIFFERENT NODE
Take POD NAME from Deployment

`kubectl get pods -o wide -l app=pod-a`

`kubectl get pods -o wide -l app=pod-b`

# TO DELETE DEPLOYMENT
`kubectl delete deployment pod-a-deployment`


