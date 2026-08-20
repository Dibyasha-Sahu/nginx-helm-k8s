# nginx-helm-k8s 🚀

A simple Helm-based deployment project to deploy an Nginx application on Kubernetes.

## 📌 Project Overview

In this project, I created a Helm chart to deploy an Nginx application on Kubernetes.

The main purpose of using Helm was to avoid managing hardcoded Kubernetes YAML files. Instead of manually changing Kubernetes manifests whenever configuration changes are required, I used Helm templates with `values.yaml` to make the deployment configurable and reusable.

## 🎯 Problem Without Helm

In traditional Kubernetes deployments, we manually modify YAML files whenever we need to change:

- Number of replicas
- Container image version
- Service configuration
- Deployment settings

This becomes difficult when managing multiple environments.

## 💡 Solution Using Helm

Helm allows us to:

- Store configurable values inside `values.yaml`
- Use templates instead of static Kubernetes YAML files
- Deploy and upgrade applications easily
- Maintain different configurations using the same chart

## 🏗️ Project Architecture
      
      Developer
        |
        |
        Helm Chart
        |
        |
        values.yaml
        |
        |
        Templates
        |
        |
        Kubernetes Resources
        |
        |
        Nginx Deployment
        |
        |
        Nginx Pods + Service

## 🛠️ Technologies Used

        - Kubernetes
        - Helm
        - Docker
        - Kind (Kubernetes in Docker)
        - kubectl

## 📂 Project Structure

        nginx-helm-k8s/

        ├── Chart.yaml
        ├── values.yaml
        │
        └── templates/
        ├── deployment.yaml
        ├── service.yaml
        └── _helpers.tpl


## 📄 Helm Chart Components

### Chart.yaml

Contains metadata about the Helm chart:

        - Chart name
        - Chart version
        - Application information


### values.yaml

Stores configurable deployment values:

Example:

        ```yaml
        replicaCount: 2

        image:
        repository: nginx
        tag: latest

        service:
        type: NodePort
        port: 80

These values are used by Helm templates during deployment.

templates/deployment.yaml

Defines the Kubernetes Deployment resource.

It uses Helm variables instead of hardcoded values.

Example:

replicas: {{ .Values.replicaCount }}

Helm replaces these values from values.yaml during deployment.

templates/service.yaml

Creates a Kubernetes Service to expose the Nginx application.

🚀 Deployment Steps
1. Create Kubernetes Cluster

Using Kind:

kind create cluster --name nginx-cluster

Verify:

kubectl get nodes
2. Install Helm Chart

Navigate to the project directory:

cd nginx-helm-k8s

Install the application:

helm install nginx-app .
3. Verify Deployment

Check Helm release:

helm list

Check Kubernetes pods:

kubectl get pods

Check service:

kubectl get svc
4. Access Nginx Application

Forward the service port:

kubectl port-forward svc/nginx-service 8080:80

Open:

http://localhost:8080

Expected output:

Welcome to nginx!
🔄 Updating Deployment Using Helm

One of the main advantages of Helm is updating applications without manually editing Kubernetes YAML files.

Example:

Change replica count in:

values.yaml

Before:

replicaCount: 2

After:

replicaCount: 5

Apply changes:

helm upgrade nginx-app .

Verify:

kubectl get pods

Helm automatically updates the Kubernetes deployment.

🔙 Helm Rollback

Helm maintains deployment history.

Check history:

helm history nginx-app

Rollback:

helm rollback nginx-app 1
🧹 Cleanup

Remove Helm deployment:

helm uninstall nginx-app

Delete Kubernetes cluster:

kind delete cluster --name nginx-cluster
📚 Key Learnings

Through this project, I learned:

✅ Creating and managing Helm charts
✅ Difference between Kubernetes YAML and Helm templates
✅ Using values.yaml for configurable deployments
✅ Deploying applications using Helm
✅ Performing Helm upgrades and rollbacks
✅ Managing Kubernetes resources efficiently

👨‍💻 Author

Dibyasha Sahu

🔖 Tags

#DevOps #Kubernetes #Helm #Docker #CloudNative #AWS