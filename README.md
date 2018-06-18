# tek-tank Kubemotion training 

This repository contains the support files used at the Kubemotion training on June 18 2018.

The following commands are the roadmap used during the workshop:

```bash
# Export the following var changing the workshop_number with your id/number.
export KOPS_STATE_STORE=s3://kops.kubemotion.com

# Export the training number, that would be provided by the trainer.
export TRAINING_NUMBER=XX

# Export a name for the cluster changing the workshop_number with your id/number.
export NAME=tek-tank-$TRAINING_NUMBER.kubemotion.com

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

cd /home/ec2-user/jenkins/services
kubectl create -f .

cd /home/ec2-user/jenkins/deployments
kubectl create -f .

# Scale the web application service.
kubectl scale --replicas=10 deployment/jenkins

# SSH into the jenkins pod
kubectl exec -t -i pod_name -- /bin/sh

# Update deployment image.
kubectl set image deployment/jenkins jenkins=jenkins/jenkins:2.127-alpine

# Create the prometheus configuration.
kubectl create -f prometheus-configmap.yaml

# Create the prometheus deployment.
kubectl create -f prometheus-deployment.yaml

# Create the prometheus service.
kubectl create -f prometheus-service.yml

# Create the grafana deployment.
kubectl create -f grafana-deployment.yaml

# Create the grafana service.
kubectl create -f grafana-service.yaml

# Get the AWS Elastic Balancer URL from the prometheus service.
kubectl describe svc prometheus

# Get the AWS Elastic Load Balancer URL from the grafana service.
kubectl describe svc grafana
```
