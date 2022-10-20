# Kubernetes - ***Pods***

- A pod is a single instance of an application and is the simplest object you can create in kubernetes

- pods usually have a 1:1 relationship with containers

- a pod can have multiple containers, but they are usually containers of different types that are tightly coupled

<br>

___

<br>

## ***Basic Commands***

<br>

- get minimal info about pods on cluser

    ```
    kubectl get pods
    ```

- get more info about a pod

    ```
    kubectl get pods -o wide
    ```

- get even more information about a pod

    ```
    kubectl describe pod <pod name>
    ```

- get pod in yaml format

    ```
    kubectl get pod <pod name> -o yaml
    ```

- enter a pod

    ```
    kubectl exec -it <pod name> -- /bin/bash
    ``` 

- create a pod
  
      ```
      kubectl run <pod name> --image=<image name>
      ```

- edit a pod
  
      ```
      kubectl edit pod <pod name>
      ```
  - If you are not given a pod definition file, you may extract the definition to a file using the below command, then edit the file to make the necessary changes, delete and re-create the pod.

      ```
      kubectl get pod <pod name> -o yaml > pod-definition.yaml
      ```

- delete a pod

    ```
    kubectl delete pod <pod name>
    ```

- view the containers user in a pod

    ```
    kubectl exec <pod name> -- whoami
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

<br>

## **Define Security Context For A Container**

  ```
  spec:
    containers:
    - name: <container name>
      image: <image name>
      securityContext:
        runAsUser: 1000
        capabilities:
          add: ["MAC_ADMIN"]
  ```

- capabilties are a set of linux kernel capabilities that can be added to or removed from a container

- capabilities are only available at the container level, not at the pod level
