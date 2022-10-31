# <img src="../../assets/img/k8s.png" width="30px"> **Kubernetes** - ***Stateful Sets*** 🌟

## **Description** 👀

`Stateful sets` are used to manage stateful applications. They are similar to deployments but they provide guarantees about the ordering and uniqueness of the pods they create. `Stateful sets` are useful for applications that require one or more of the following. Stable, *unique network identifiers*. Stable, *persistent storage*. Ordered, *graceful deployment and scaling*. Ordered, *automated rolling updates*.

<br />

## **Basic** `Commands` 📝

* **scale** a `stateful set`

    ```shell
    kubectl scale statefulset <stateful-set-name> --replicas=<number-of-replicas>
    ```

<br />

## **Examples** 🧩

* `stateful set` definition

    ```yaml
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
        name: mysql
        labels:
            app: mysql
    spec:
        replicas: 3
        selector:
            matchLabels:
                app: mysql
        serviceName: mysql-h
        # causes the pods to be created in parallel, rather than sequentially. will maintain all of its other properties.
        podManagementPolicy: Parallel
        template:
            metadata:
                labels:
                    app: mysql
            spec:
                containers:
                - name: mysql
                image: mysql
    ```

<br />

[↩️](../README.md)
