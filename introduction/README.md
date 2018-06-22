# Kubemotion workshop 

This repository contains the support and the commands that would be executed on Kubemotion's Kubernetes intro training. 

# Workshop objective

The workshop objective would be to deploy a fresh Kubernetes cluster on AWS using kops and learn about Kubernetes common operations.

# Workshop commands

The following commands are the roadmap used during the workshop:

```bash
# Export kops state store, it's a AWS bucket that kops would use to store it's state. 
export KOPS_STATE_STORE=s3://kops.kubemotion.com

# Export the training number, it would be provided by the trainer.
export TRAINING_NUMBER=XX

# Export a name for the cluste.
export NAME=workshop-$TRAINING_NUMBER.kubemotion.com

# Create the cluster configuration.
kops create cluster ${NAME} --zones eu-west-1a

# Review the cluster node configuration.
kops edit ig --name=${NAME} nodes

# Review the master node configuration.
kops edit ig --name=${NAME} master-eu-west-1a

# Launch the cluster.
kops update cluster --name=${NAME} --yes

# Validate the cluster
kops validate cluster

# See the running nodes
kubectl get nodes

# See the system running pods.
kubectl get po --all-namespaces

# Create another ssh session with a watch
watch kubectl get po --all-namespaces

# Lets deploy an application
cd /home/ec2-user/guestbook/services
kubectl create -f .

cd /home/ec2-user/guestbook/deployments
kubectl create -f .

# Scale the web application service.
kubectl scale --replicas=10 deployment/frontend

# Get the logs from a pod
kubectl logs pod_name

# SSH into a pod
kubectl exec -t -i pod_name -- /bin/sh

# Update deployment image.
kubectl set image deployment/frontend php-redis=gcr.io/google-samples/gb-frontend:v4

# Port forward a pod 
kubectl port-forward pod_name 80:80

# Cordon a node to avoid new scheduling
kubectl cordon node_name

# Drain pods from a node
kubectl drain node_name

# Delete the cluster
kops delete cluster ${NAME} --yes
```
