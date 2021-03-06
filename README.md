# Running Apache Geode on Kubernetes

Set of instructions and artifacts to get [Apache Geode](http://geode.incubator.apache.org) running on [Kubernetes](http://kubernetes.io/).

## Build Docker image to include shell scripts

Go to the `image` directory and build the Docker image using:

1. `docker build . -t <your image name and tag>`
1. `docker push <your image name and tag>`
1. Change references to the base image in each controller file to point to your personalized image

# Running on PKS

*Steps*:

1. `kubectl create -f bootstrap-configmap.yml`
1. `kubectl create -f locator-configmap.yml`
1. `kubectl create -f server-configmap.yml`
1. `kubectl create -f locator-controller.yaml`
1. `kubectl create -f locator-service.yaml`
1. `kubectl create -f server-controller.yaml`
1. `kubectl create -f server-service.yaml`
1. `kubectl create -f bootstrap-job.yml`

You can scale the number of servers by using the following command:

`kubectl scale --replicas=3 -f server-controller.yaml`

# Running Sample App

<kbd>![alt-text](https://github.com/azwickey-pivotal/geode-kubernetes/blob/master/screenshot.png)</kbd>

*Steps*:

1. `Deploy Geode to cluster (see above steps)`
1. `kubectl create -f app-service.yml`
1. `kubectl create -f app-rs.yml`
1. SSH info application pod<br>`kubectl exec -it <geode app pod name> bash`
1. Launch gfsh<br>`gfsh`
1. Connect to Geode StatefulSet<br>`gfsh>connect --locator=geode-locator[10334]`
1. Create test region for the app<br>`create region --name=/test --type=PARTITION`
