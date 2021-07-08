# simplek8s

This is the continuationor update to the previous project "Complexy". Here we will be making use of Kubernetes for the same work. 

## Get a simple container running on our local kubernetes cluster

1. make sure our image is still hosted on docker hub. 
2. Make a config file to create the container
3. Make one config file to set up networking.

The config file is a very different file to be exact.  A config file is used to create objects. 
Object serve different purposes:
- running a container
- monitoring a container
- setting up networking, etc
We have 2 files here:
1. `client-pod.yaml`
2. `client-node-port.yaml`

Some definitions:
- apiVersion : Scopes or limits the types of objects we can specify, that we want to create within a given config file. Each API version defines a different set of 'objects' we can use. 
- kind : these are the object types a config file helps create. 
         - pods : Runs one or more closely related containers
         - services : Sets up networking in a k8s cluster 

Here in this project, we're creating a pod and we're running 1 container [name: client] inside it. 
Port mapping is old-school for now, so we have the second config file for networking. 

#### Services 
There are 4 sub-types of services : 
- ClusterIP
- NodePort
- Loadbalancer
- ingress

Here, we've used `NodePort`, which exposes the container to the outside world. (allows access through a browser) 

### We're talking 'ports' in client-node-port.yaml :
There's no path defined as such,  like a legit connection to client 'pod'. Instead, rather than addressing any service or pods, or using a naming system; we use a system in k8s called a `label selector` system. 
In both files, we have a column of `component:web`. [labels in client-pod, & selector in client-node-port].
These are arbitrary and need to be same in both the config files. By this, it exposes port 3000 (here) to the outside world.
