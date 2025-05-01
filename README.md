# Kubernetes NFS-Backed HTTP Server

## Prerequisites
- kubectl
- helm
- Minikube

## How to run

```bash
# Start Minikube with docker
minikube start --driver=docker

# Install NFS provisioner
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm install my-first-release nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner  --set storageClass.name=my-nfs-storage  --set storageClass.defaultClass=true

# Apply manifests
kubectl apply -f manifests/pvc.yaml
kubectl apply -f manifests/nginx-deployment.yaml
kubectl apply -f manifests/nginx-service.yaml
kubectl apply -f manifests/job.yaml

# Get Service URL
minikube service nginx-service --url
