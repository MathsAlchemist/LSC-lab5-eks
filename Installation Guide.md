Installation of kubectl and configuration:\
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
aws eks --region us-east-1 update-kubeconfig --name MyEKSCluster
```

Installation of Helm and charts:\
```
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm repo add stable https://charts.helm.sh/stable
helm repo update
```

Installation of nfs-server-provisioner:\
```
helm install nfs-server-provisioner stable/nfs-server-provisioner \
  --set storageClass.name=nfs-storage \
  --set storageClass.defaultClass=true
```
Creating the 4 .yaml files included in the repository and running them with kubectl:\
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
