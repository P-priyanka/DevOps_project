# DevOps_project
AWS EKS High-Availability Deployment for Interdependent Applications

## Use these commands during the demo

## Install aws cli
`sudo apt get install awscli`

## Temporarily change editor (optional)
export EDITOR=nano

## Edit aws lab config
`subl ~/.aws/credentials`

From awsacademy account and copy the credentials to this file(replace all there is by default)

## Connect to the cluster
`aws eks --region us-west-2 update-kubeconfig --name eks1`

## Create a namespace
`k create ns podns`

## Set default namespace
`k config set-context --current --namespace=podns`

# PROMETHEUS AND GRAFANA

## Install openssl
`sudo yum install openssl -y`

## Install helm 
`curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3`

`chmod 700 get_helm.sh`

`./get_helm.sh`

## create a namespace
`kubectl create namespace prometheus`

## Add grafana to repo
`helm repo add grafana https://grafana.github.io/helm-charts`

## Install prometheus-stack
``` bash helm install my-kube-prometheus-stack prometheus-community/kube-prometheus-stack \
--create-namespace --namespace prometheus \
--set prometheus.service.type=LoadBalancer \
--set prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues=false \
--set grafana.service.type=LoadBalancer \
--set grafana.adminpassword=password
```

## To see all prometheus details
`kubectl get all -n prometheus`

## Open prometheus & grafana locally
`kubectl port-forward deployment.apps/my-kube-prometheus-stack-grafana -n prometheus 8080:80`

`kubectl port-forward svc/prometheus-operated -n prometheus 8081:9090`

## To get Grafana credentials
`kubectl get secret my-kube-prometheus-stack-grafana -n prometheus -o jsonpath="{.data.admin-user}" | base64 --decode ; echo`

`kubectl get secret my-kube-prometheus-stack-grafana -n prometheus -o jsonpath="{.data.admin-password}" | base64 --decode ; echo`

## Open grafana by IP
## Import Dashboard Kubernetes EKS Cluster to see better view









