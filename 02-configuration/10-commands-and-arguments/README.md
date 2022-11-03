# <img src="../../assets/img/k8s.png" width="30px"> **Kubernetes** - ***Commands*** *and* ***Arguments*** 🔣

## **Description** 👀

To pass arguments to a `container`, you can use the `args` field of the `container spec`. Arguments to the entrypoint can be passed using the `command` field of the `container spec`.

* *example* `container` *cmd-and-args-example/Dockerfile*
* *example* `pod definition` *cmd-and-args-example/pod-definition.yaml*

<br />

## ***Docker*** `Commands` *and* `Arguments` 🐳

* generic `DOCKERFILE` template

  ```Dockerfile
  FROM <image>
  RUN <command>
  CMD <command>
  ```

* commands template with parameters

  ```Dockerfile
  CMD command param
  CMD ["command", "param"]
  ```

* example command with arguments

  ```Dockerfile
  CMD sleep 5
  CMD ["sleep", "5"]
  ```

* makes a custom image of ubuntu and makes it sleep 5 seconds then exits

  ```Dockerfile
  FROM Ubuntu
  CMD sleep 5
  ```

* makes a custom image of ubuntu and makes it sleep from passed in param in entrypoint
  * entrypoint is the command that is run when the container is started

  ```Dockerfile
  FROM Ubuntu
  ENTRYPOINT ["sleep"]
  ```

* makes a custom image of ubuntu and makes it sleep from passed in param in entrypoint with default of 5 seconds

  ```Dockerfile
  FROM Ubuntu
  ENTRYPOINT ["sleep"]
  CMD ["5"]
  ```

  * you can override the entrypoint command with the --entrypoint flag

* ***Docker*** `Security` 🔒

  * to run docker as a non-root user

    ```bash
    docker run --user=<user id> <image>
    ```

  * users can also be defined in the dockerfile

    ```Dockerfile
    FROM ubuntu
    USER <user id>
    ```


<br />

## **Examples** 🧩

* sample `Dockerfile` 🐳

    ```Dockerfile
    FROM ubuntu
    ENTRYPOINT [ "sleep" ]
    CMD [ "5" ]
    ```

* sample `pod` definition with `container` *commands* and *arguments*

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

<br />

[↩️](../README.md)
