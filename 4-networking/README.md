# Kubernetes - ***Networking***

* A node has an IP address that is used to communicate with other nodes in the cluster
* If you are using minikube you can get the IP address of the node by running ```minikube ip```
* When kubernetes is configured ip addresses are assigned to pods
  * Pods can communicate with each other using their IP addresses
  
Kubernetes expects you to follow fundamental networking principles when you create your applications.  These principles are:

  * All containers/ pods can communicate to one another without NAT
  * All nodes can communicate with all containers without NAT and vice versa

Some out of the box solutions include:

* Flannel
* calico
* vmware NSX
  
  