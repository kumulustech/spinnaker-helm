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


### Note: If you use minikube, increase the memory, disk size, and if you have them, the available CPUs:

    minikube config set memory 8192
    minikube config set disk-size 30GB
    minikube config set cpus 4

### Second Note, if you have less than 12GB memory (physical) in your machine don't waste your time, it will not work.
Gitclone the lab repo:

git clone https://github.com/kumulustech/spinnaker-helm spinnaker

cd spinnaker

Launch:

1) Install helm:

    helm init --upgrade

2) Install RBAC rules:

    kubectl create -f rbac.yml

3) Launch Spinnaker (and minio, redis, jenkins)
    Note: If you get "Error: could not find a ready tiller pod" wait a minute and try run the command again.
    
    helm install --name spinnaker spinnaker/
    
Then follow the output of the helm install.

=================================================

### Restarting a failed Spinnaker deployment.
In some cases, you may end up with a deployment that has some microservices (pods) in an error state after your deployment has completed. (e.g. "Error: timed out waiting for the condition") 
In this case you will want to run:

helm del --purge spinnaker

Before redeploying Spinnaker with Helm, check that your environment is cleaned up. In particular, check that there are no PVCs present

kubectl get pvc

and that the only secret present is the kubernetes default token  (Type:kubernetes.io/service-account-token) 

kubectl get secrets

Delete any extra PVCs or secrets.
Now rerun 

helm install --name spinnaker spinnaker/
