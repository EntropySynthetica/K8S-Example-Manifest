# K8S-Example-Manifest
A basic K8S deployment to use as an example, or testing new clusters.  


# Get this deployment up and running.  

A basic K8S project consists of 3 parts.  A deployment, a serivce and an ingress.  The deployment specifies what docker image to run, how many copies, as well as rules that specify how containers will be replaced if there is a failure or upgrade to the deployment.   The service exposes networking of the deployment.  It gives a handy single point of reference for other objects in the k8s cluster to talk to one or multiple pods.  And finally the Ingress is an http/https load balancer that exposes the cluster to the outside world.  The ingress rules tell K8S what URL should go to what workload.  

## Verify your kubectl command is connected to your cluster.  

You should be able to do a `kubectl get nodes` and get a non-error response.  

## Apply the deployment

Run `kubectl apply -f deploy.yaml`

You can check on the status of the deploy with `kubectl get deploy`
You can also check on the pods in this deploy with `kubectl get pods`

## Apply the service

Run `kubectl apply -f service.yaml`

You can verify the status of the service with `kubectl get service`

## Apply the Ingress Rules

Run `kubectl apply -f ingress.yaml`



## Setup ingress.  

In your hosts file or on your DNS server you need to setup arule so `helloworld.local` is pointed to the IP of your Kubernetes cluster.  If you have multiple nodes pointing the IP to any worker node will work.  

You should then be able to visit http://helloworld.local in your browser and see the service.  


## Teardown

You can remove everything by applying the manifest files to a delete command. 

* `kubectl delete -f deploy.yaml`
* `kubectl delete -f service.yaml`
* `kubectl delete -f ingress.yaml`

You can also delete with the names of the deploy, service and ingerss

* `kubectl delete deploy helloworld`
* `kubectl delete service helloworld-service`
* `kubectl delete ingress helloworld-ingress`