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

  * get pod in yaml format

    ```
    kubectl get pod <pod name> -o yaml
    ```

  * create a pod 
  
      ```
      kubectl run <pod name> --image=<image name>
      ```

  * edit a pod
  
      ```
      kubectl edit pod <pod name>
      ```
    * If you are not given a pod definition file, you may extract the definition to a file using the below command, then edit the file to make the necessary changes, delete and re-create the pod.
      ```
      kubectl get pod <pod name> -o yaml > pod-definition.yaml
      ```

  * delete a pod

    ```
    kubectl delete pod <pod name>
    ```

<br>

## ***Define Enviroment Variables For A Container***

<br>


  ```  
  spec:
    containers:
    - name: <container name>
      image: <image name>
      env:
      - name: DEMO_GREETING
        value: "Hello from the environment"
      - name: DEMO_FAREWELL
        value: "Such a sweet sorrow"
  ```