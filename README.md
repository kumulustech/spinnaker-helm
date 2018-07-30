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
