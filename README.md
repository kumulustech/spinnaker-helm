# A helm chart for spinnaker

This is not a new chart, rather it is the standard chart, working...

These charts are pulled from https://github.com/helm/charts/stable
* spinnaker
* minio
* jenkins
* redis

Fixes include:
 - service names that match expectations for spinnaker services
   - minio-svc
   - redis-svc
 - redis password naming for spinnaker config and redis


### Note: If you use minikube, increase the memory, and if you have them, the available CPUs:

    minikube config set memory 8192
    minikube config set cpus 4

### Second Note, if you have less than 8GB memory (physical) in your machine don't waste your time, it will not work.

Launch:

1) Install helm:

helm init --upgrade

2) Install RBAC rules:

kubectl create -f rbac.yaml

3) Launch Spinnaker (and minio, redis, jenkins)

    git clone https://github.com/kumulustech/spinnaker-helm spinnaker
    
    helm install --name spinnaker spinnaker/ --timeout 500

Then follow the output of the helm install.
