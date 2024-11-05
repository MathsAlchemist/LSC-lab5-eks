Creation of EKS cluster:
1. Enter AWS Management Console
2. Create Role for EKS if not exists
3. Add AmazonEKSClusterPolicy policy
4. Create EKS Cluster
5. Choose role mentioned in point 2
6. Default setting should work fine for the rest of the options
7. Go to Compute tab
8. Create a new node group with the configuration that suits you
9. Use role with AmazonEKSWorkerNodePolicy, AmazonEC2ContainerRegistryReadOnly polices
10. Then move to the installation below

Installation of kubectl and configuration:
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
aws eks --region us-east-1 update-kubeconfig --name MyEKSCluster
```

Installation of Helm and charts:
```
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm repo add stable https://charts.helm.sh/stable
helm repo update
```

Installation of nfs-server-provisioner:
```
helm install nfs-server-provisioner stable/nfs-server-provisioner \
  --set storageClass.name=nfs-storage \
  --set storageClass.defaultClass=true
```
Creating the 4 .yaml files included in the repository and running them with kubectl:
```
kubectl apply -f pvc.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f job.yaml
```

Checking the ip of nginx service:
```
kubectl get service nginx-service
```
