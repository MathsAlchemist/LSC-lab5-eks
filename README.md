Kubernetes deployment (5p)

a) Create a k8s cluster using Amazon Elastic Kubernetes Service (EKS)
\
· You can also use minikube, kind, or any other Kubernetes distribution, or existing cluster.\
· Minikube, by default, uses its own internal Docker daemon. This daemon doesn’t know anything about images built previously. Prepare your environment by directing it to access the internal docker daemon by using the $(minikube docker-env) command and rebuild your images. This way images will be available within the k8s cluster. (https://medium.com/bb-tutorials-and-thoughts/how-to-use-own-local-doker-images-with-minikube-2c1ed0b0968) \
\
b) Using Helm, install an NFS server and provisioner in the cluster.

· Go to charts/nfs-server-provisioner for a README.\
· Pay attention to configuration parameters, in particular, override storageClass.name which denotes the name of the StorageClass that you’ll have to use when creating Persistent Volume Claims. \
\
c) Create a Persistent Volume Claim which will bind to a NFS Persistent Volume provisioned dynamically by the provisioner installed in the previous step. \
d) Create a Deployment with a HTTP server (e.g., apache or nginx). The web content directory should be mounted as a volume using the PVC created in the previous step. \
e) Create a Service associated with the Pod(s) of the HTTP server Deployment. \
f) Create a Job which mounts the PVC and copies a sample content through the shared NFS PV.\
g) Test the HTTP server by showing the sample web content in a browser.
