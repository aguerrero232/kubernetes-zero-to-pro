# Kubernetes - ***Pods***

- A pod is a single instance of an application and is the simplest object you can create in kubernetes

- pods usually have a 1:1 relationship with containers

- a pod can have multiple containers, but they are usually containers of different types that are tightly coupled 

<br>

___

<br>

## ***Basic Commands***

<br>

  * get minimal info about pods on cluser

    ```
    kubectl get pods
    ```

  * get more info about a pod

    ```
    kubectl get pods -o wide
    ```

  * get more information about a pod

    ```
    kubectl describe pod <pod name>
    ```

  * delete a pod

    ```
    kubectl delete pod <pod name>
    ```