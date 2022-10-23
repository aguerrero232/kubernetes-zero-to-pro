# **Kubernetes** - ***Commands and Arguments*** 🔣

To pass arguments to a `container`, you can use the `args` field of the `container spec`. Arguments to the entrypoint can be passed using the `command` field of the `container spec`.

* *example* `container` *cmd-and-args-example/Dockerfile*
* *example* `pod definition` *cmd-and-args-example/pod-definition.yaml*


<br>

## ***Basic*** `Commands` 📝

* build docker container

    ```bash
        docker build  -t <container-name>  .
    ```

<br />

## **Examples** 📚

* sample `Dockerfile`

    ```Dockerfile
    FROM ubuntu
    ENTRYPOINT [ "sleep" ]
    CMD [ "5" ]
    ```

* sample `pod` definition

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: ubuntu-sleeper-pod
    spec:
        containers:
          - image: ubuntu-sleeper
            name: ubuntu-sleeper
            # overrides the entrypoint instruction 
            command: ["echo"]  
            # overrieds the commad instruction  
            args: ["10"]
    ```
