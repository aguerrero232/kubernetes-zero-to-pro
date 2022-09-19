# Kubernetes for Beginners

## Valuable Links

* ***[kubernetes concepts](https://kubernetes.io/docs/concepts/)***

<br>

___
## Kubernetes Architecture

<br>

***Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.***

<br>

![](img/clusterdiagram2.PNG) ![](img/clusterdiagram-legend.PNG)

<br/>

* The **Control Plane** is responsible for managing the cluster. 
    * Components: 
      * kube-apiserver - Exposes the Kubernetes API
      * etcd - Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
      * kube-scheduler - Watches for newly created Pods with no assigned node, and selects a node for them to run on.
      * kube-controller-manager - Runs controller processes. Each controller is a separate process but to keep things simple they are compiled together and run in a single process
        * Examples: 
            * Node controller: Responsible for noticing and responding when nodes go down.
            * Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
            * Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
            * Service Account & Token controllers: Create default accounts and API access tokens for new namespaces

      * cloud-controller-manager - Embeds cloud-specific control logic
        * Node, Route, and Service controllers can have cloud provider dependancies.
      
<br/>

* A **Node** is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster.
    * The nodes communicate with the control plane using the Kubernetes API

    * Components: 
      * kubelet - An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
      * kube-proxy - Network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.
      * Container runtime - Software that is responsible for running containers.

<br>

___
## ***Basic Commands***

<br>

* ## **minikube commands**

  * Check the status of minikube

    ```
    minikube status
    ```
  * Start minikube

    ```
    minikube start
    ```

  * Stop minikube

    ```
    minikube stop
    ```

<br>

* ## **kubectl commands**

  * check version of kubernetes being used
    
    ```
      kubectl version
    ```

  * get minimal info about pods on cluser

    ```
      kubectl get pods
    ```

  * get more info about pods on cluster, IP and Node where pod is running

    ```
      kubectl get pods -o wide
    ```

  * get more information about a pod on cluser

    ```
      kubectl describe pod <pod name>
    ```
  * run a new pod

    ```
      kubectl run <pod name> --image <image name>
    ```
  * run a new pod using a yaml file

    ```
      kubectl apply -f <file name>
    ```

  * delete a pod from cluster

    ```
      kubectl delete pod <pod name>
    ```


  * create a new deployment

    ```
      kubectl create deployment <pod name> --image=<image name>
    ```
<br>

* ## **Other usefull commands**

  * view the flavor and version of OS
    ```
      cat /etc/os-release
    ```


  