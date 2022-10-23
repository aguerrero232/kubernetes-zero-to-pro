# **Kubernetes** - ***ConfigMaps*** 🗺️

Just like everything else in kubernetes there are two ways to create a `ConfigMap`. You can either use the `kubectl` command or you can use a `ConfigMap` manifest file.

* example at `yaml-examples/configmap-description.yaml`

To tie a `ConfigMap` to a **Pod** you can use the `envFrom` or `env` section of the **Pod** manifest file.

* example at `yaml-examples/configmap-pod.yaml`

<br>

## ***Basic*** `Commands` 📝

* **create** a `ConfigMap` using the `kubectl` command,

    ```bash
    kubectl create configmap <configmap-name> --from-literal=<key>=<value>
    ```

* **create** a `ConfigMap` using a `manifest file`,

    ```bash
    kubectl create configmap <configmap-name> --from-file=<path-to-file>
    ```

* **get** a `ConfigMap`

    ```bash
    kubectl get configmap <configmap-name>
    ```

* **describe** a `ConfigMap`

    ```bash
    kubectl describe configmap <configmap-name>
    ```

* **delete** a `ConfigMap`

    ```bash
    kubectl delete configmap <configmap-name>
    ```

<br>

## **Examples** 📚

* sample `ConfigMap`

    ```yaml
    APP_COLOR: blue
    APP_MODE: production
    ```

* sample `ConfigMap` manifest file

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
        name: sample-config
    data:
        APP_COLOR: blue
        APP_MODE: production
    ```

* sample `Pod` manifest file

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: configmap-pod
    spec:
        containers:
          - name: configmap-container
            image: nginx
            ports:
              - containerPort: 80
            envFrom:
              - configMapRef:
                    name: sample-config
    ```
