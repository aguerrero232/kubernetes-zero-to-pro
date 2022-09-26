# Kubernetes - ***Imperative Commands***

Imperative commands can help in getting one time tasks done quickly, as well as generate a definition template easily. 


Familiarize yourself with the following commands:

* `--dry-run` 
  * will execute, and the resource will be created.

* `--dry-run=client`
  * will execute, but the resource will not be created.

* `-o yaml`
  * will output the resource definition in yaml format.

<br>

___

<br>

## **Basic Commands**

<br>

**Use in combination to generate a resource definition file quickly, that you can then modify and create resources as required, instead of creating the files from scratch.**

<br>


* create a pod manifest file
    ```
    kubectl run <pod name> --image=<image name> --dry-run=client -o yaml
    ``` 

* create a deployment manifest file

    ```
    kubectl create deployment --image=<image name> --dry-run=client -o yaml
    ```

* create a service manifest file

    ```
    kubectl expose <object type> <object name> --port=<port> --name <service name> --dry-run=client -o yaml
    ```



**Example:**

* **Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:**

    ```

    kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
    ```

    (This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.)