# Stateful-Application-deployment-on-Kubernetes
## 1. Create a Namespace on the cluster
 Multiple teams and projects are already using this a single Kubernetes cluster. To isolate the resources and prevent any naming conflicts, create a new namespace.
   ```
   kubectl create <namespace>
   ```
   you can store the configuration required to create the namespace in a Kubernetes manifest file and using that you can create the namespace
   ```
   kubectl create <namespace> --dry-run=client -o yaml > <namespace.yaml>

   kubectl create -f <namespace.yaml>
   ```
if you want to set the new workspace as the preferred workspace
```
kubectl config set-context --current --namespace=<namespace>
```
## 2. Create a Kubernetes deployment for MongoDB
The appplication that you want to deploy requires a MongoDB database for storing data. I used the MongoDB version 6.0.3. Use kubectl to deploy the MongoDB database by employing imperative commands.
 ```
kubectl create deployment <mongo-deployment> --image=mongo:6.0.3
```
using the manifest file
```
kubectl create deployment mongo-deployment --image=mongo:6.0.3 --dry-run=client -o yaml > k8s-mongo-deployment.yaml
kubectl create -f k8s-mongo-deployment.yaml
kubectl get pods
   ```
## 3. Configure the MongoDB container with environment variables
Expand the Kubernetes manifest file for the MongoDB deployment to include the following environment variables that are required to configure access to the database.
```
    spec:
      containers:
      - image: mongo:6.0.3
        name: mongo
        resources: {}
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          value: "mongoadmin"
        - name: MONGO_INITDB_ROOT_PASSWORD
          value: "secret"
```
After making the necessary changes replace the existing deployment with the new configuration
```
kubectl replace -f FILENAME

```
## 4. Expose MongoDB within the cluster
Create a Kubernetes service that exposes the deployment on port 27017 using kubectl expose. Ensure that the service type is ClusterIP and the name of the service, mongo-service. 
```
kubectl expose deployment mongo-deployment --name=mongo-service --type=ClusterIP --port=27017
kubectl get services
```
To store the configuration required to create the service in a Kubernetes manifest file, use the same command which you have used to create the service, but this time use the --dry-run flag to prevent the execution and store the output as YAML to a file named k8s-mongo-service.yml. The entire command will look as follows:
```
kubectl expose deployment mongo-deployment --name=mongo-service --type=ClusterIP --port=27017 --dry-run=client -o yaml > k8s-mongo-service.yaml
```
command to create the deployment from the file containing the manifest.
```
kubectl create -f k8s-mongo-service.yaml
```
## 5. Store private Docker registry credentials
## 6. Create a Kubernetes deployment for EMP
## 7. Configure EMP to use MongoDB
## 8. Expose EMP using a Load Balancer
## 9. Manual acceptance test
## 10. Configure Secrets for storing MongoDB credentials
## 11. Configure EMP to use Secrets when authenticating to MongoDB
## 12. Configure ConfigMaps for storing MongoDB connection details
## 13. Configure EMP to use ConfigMaps when connecting to MongoDB
## 14. Create a Persistent Volume for storing application data
## 15. Configure MongoDB to use a PersistentVolume






