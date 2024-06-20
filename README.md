# Stateful-Application-deployment-on-Kubernetes
1. Create a Namespace on the cluster
2. Store the configuration required to create the namespace in a Kubernetes manifest file using the YAML format. Then set the new workspace as the preferred workspace.Make sure to use the imperative approach for managing Kubernetes objects


 ```
   "kubectl create <namespace>"
    vi <file-name.yaml>
kubectl create deployment mongo-deployment --image=mongo:6.0.3

kubectl create deployment mongo-deployment --image=mongo:6.0.3 --dry-run=client -o yaml > k8s-mongo-deployment.yaml
kubectl delete deployment/mongo-deployment

kubectl create -f k8s-mongo-deployment.yaml


   ```
