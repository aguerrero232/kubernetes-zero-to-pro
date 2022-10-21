# **Kubernetes** `-` ***ConfigMaps***

<br>

Just like everything else in kubernetes there are two ways to create a `ConfigMap`. You can either use the `kubectl` command or you can use a `ConfigMap` manifest file.

* example at `yaml-examples/configmap-description.yaml`

To tie a `ConfigMap` to a **Pod** you can use the `envFrom` or `env` section of the **Pod** manifest file.

* example at `yaml-examples/configmap-pod.yaml`

<br>

## ***Basic*** `Commands`

<br>

* **create** a `ConfigMap` using the `kubectl` command,

    ```shell
    kubectl create configmap <configmap-name> --from-literal=<key>=<value>
    ```

* **create** a `ConfigMap` using a `manifest file`,

    ```shell
    kubectl create configmap <configmap-name> --from-file=<path-to-file>
    ```

* **get** a `ConfigMap`

    ```shell
    kubectl get configmap <configmap-name>
    ```

* **describe** a `ConfigMap`

    ```shell
    kubectl describe configmap <configmap-name>
    ```

* **delete** a `ConfigMap`

    ```shell
    kubectl delete configmap <configmap-name>
    ```
