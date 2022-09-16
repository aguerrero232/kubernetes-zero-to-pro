# Kubernetes - ***Pods***

- A pod is a single instance of an application and is the simplest object you can create in kubernetes

- pods usually have a 1:1 relationship with containers

- a pod can have multiple containers, but they are usually containers of different types that are tightly coupled 

<br>

___

<br>

## **Example of a simple pod defined in a yaml file:**

<br>

```
    apiVersion: v1

    # kind refers to the type of object that will be created
    kind: Pod

    # data about the data that will be created
    metadata:
    name: myapp-pod
    labels:
        app: myapp
        type: testing

    # specification section, providing additional information to kubernetes about the object
    spec:
    containers:
        - name: nginx-container
          image: nginx
```
