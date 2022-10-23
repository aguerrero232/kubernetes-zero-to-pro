# **Kubernetes** - ***Resource Requirements*** 💾

`Resources` are the compute, storage, and network `resources` that are required by containers. Kubernetes allows you to specify the amount of `resources` that a container requires. This allows Kubernetes to schedule containers on nodes that have enough `resources` to run the containers. Kubernetes also allows you to specify the limits of the `resources` that a container can use. This allows Kubernetes to prevent containers from using more `resources` than they are allowed to use.

Limits and Requests for `resources` are specified in the `resources` section of a container's `spec`. The `resources` section has two sub-sections: `requests` and `limits`. The `requests` section specifies the minimum `resources` that a container needs to run. The `limits` section specifies the maximum `resources` that a container can use.

`Kubernetes` allows `Pods` to specify default resources for a container. These default resources are used when a container does not specify its own resource requirements. The default resources are specified in the `spec` section of a Pod's `spec`.

<br />

## **Examples** 📚

* sample `pod` with `resource requirements` manifest file

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: myapp
        labels:
            name: myapp
    spec:
        containers:
          - name: myapp
            image: nginx
            resources:
                requests:
                    memory: "64Mi"
                    cpu: "250m"
                limits:
                    memory: "128Mi"
                    cpu: "500m"
    ```

<br>

[↩️ **back**](../)
