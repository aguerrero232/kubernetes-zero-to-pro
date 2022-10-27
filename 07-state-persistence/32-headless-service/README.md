# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Headless Service*** 🧟

## **Description** 👀

A `headless service` is a service that does not have a `ClusterIP`. This means that the service will not have a virtual IP address. Instead, the service will return the `Pod` IP addresses. This is useful for stateful applications that require a stable IP address for each `Pod`.

<!-- 
<br />

## **Basic** `Commands` 📝 -->

<br />

## **Examples** 🧩

* `headless service` definition

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
        name: mysql-h
    spec:
        ports:
        - port: 3306
        selector:
            app: mysql
        clusterIP: None
    ```

  * `headless service` does not have a `ClusterIP`, must set `clusterIP` to **None**

* `pod` using `headless service`

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: myapp-pod
        labels:
            app: mysql
    spec:
        containers:
          - name: mysql
            image: mysql
        # pod uses headless service
        subdomain: mysql-h
        hostname: mysql-pod
    ```

* `stateful set` using `headless service`

    ```yaml
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
        name: mysql-deployment
        labels:
            app: mysql
    spec:
        serviceName: mysql-h
        replicas: 3
        selector:
            matchLabels:
                app: mysql
        template:
            metadata:
                name: myapp-pod
                labels:
                    app: mysql
            spec:
                containers:
                  - name: mysql
                    image: mysql
    ```

  * `serviceName` is the name of the `headless service` that the `stateful set` will use
  * the stateful set does not need to specify the `subdomain` and `hostname` because the `stateful set` will automatically create a `headless service` for each `pod` in the `stateful set`

* `stateful set` using `headless service` with `pvc` for each `pod`

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
        template:
            metadata:
                labels:
                    app: mysql
            spec:
                containers:
                  - name: mysql
                    image: mysql
                    volumeMounts:
                      - name: data-volume
                        mountPath: /var/lib/mysql
        volumeClaimTemplates:
          - metadata:
                name: data-volume
            spec:
                accessModes:
                    - ReadWriteOnce
                storageClassName: google-storage
                resources:
                    requests:
                        storage: 500Mi
    ```

  * `volumeClaimTemplates` is used to create a `pvc` for each `pod` in the `stateful set`
  * `stateful sets` do not automatically delete `pvc` when  `pods` fail or are deleted, instead they ensure that when the `pod` is recreated, the `pvc` is bound back to the `pod` that was recreated.

<br />

[↩️](../README.md)
