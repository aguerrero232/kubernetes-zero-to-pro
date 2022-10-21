# **Kubernetes** `-` ***Commands and Arguments***

<br>

To pass arguments to a `container`, you can use the `args` field of the `container spec`. Arguments to the entrypoint can be passed using the `command` field of the `container spec`.

* *example* `container` *cmd-and-args-example/Dockerfile*
* *example* `pod definition` *cmd-and-args-example/pod-definition.yaml*


<br>

## ***Basic*** `Commands`

<br>


* build docker container

    ```shell
        docker build  -t <container-name>  .
    ```
