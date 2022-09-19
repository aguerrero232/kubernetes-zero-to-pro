# Kubernetes - ***Deployments***

Deployments are the preferred way to manage pods. They are a **higher level abstraction** than Replica Sets. They allow you to define the desired state of your application, and the controller will make sure that the current state matches the desired state. 

<br>

___

<br>

## ***Basic Commands***

* create a new deployment

    ``` 
    kubectl create -f <yaml file>
    ```

* get list of deployments

    ```
    kubectl get deployments
    ```

* get descriptive information on the desired deployment

    ```
    kubectl describe deployment <deployment name>
    ```

