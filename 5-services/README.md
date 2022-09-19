# Kubernetes - ***Services***

A service is a way to expose an application running on a set of pods as a network service. It is services that enables connectivity between pods and external clients.

<br>

___

<br>


## ***Types of Services***

<br>


  * NodePort
    * makes an internal port accessible on the node
    * uses 3 ports
      * 1 port on the node, the node port
        * the node ports range is between 30000-32767
      * 1 port on the pod, the target port
      * 1 port on the service, the service port

<br>

  * ClusterIP
    * The service creates a virtual IP inside the cluster that allows other pods to communicate with it 
    * helps provide a single interface to a set of pods 

<br>

  * LoadBalancer
    * Provisions a load balancer
    * only works on cloud providers that support native load balancers
    

___

<br>

## ***Basic Commands***

<br>

* create a service
    ```
    kubectl create -f  <yaml file>
    ```

* get list of services
    ```
    kubectl get services
    ```

* get descriptive information on the desired service
    ```
    kubectl describe service <service name>
    ```


* access service ```in browser``` running on minikube 
    ```
    minikube service <service name> --url
    ```
