
# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Persistent Volume Claims*** 🚩

## **Description** 👀

`Persistent Volume Claims`, otherwise known as `PVC`, and `Persistent Volumes` are two separate `Kubernetes` resources. `PVC` are a way to *dynamically provision* from a `persistent volume` based on the request and properties set on the volume such as `size`, `access mode`, `storage class`, etc. `PVC` are also used to *bind* `persistent volumes` to `pods` and `containers` in order to *persist* data. `PVC` are also used to *reclaim* `persistent volumes` when they are no longer needed. **Every** `PVC` is bound to a single `persistent volume`. There is a **1:1** relationship between `PVC` and `persistent volumes`.

<!-- are a way to *request* a `persistent volume` from the `cluster`. `Persistent Volume Claims` are a resource that is independent of the `pod` lifecycle. This means that `Persistent Volume Claims` can be created, used, and destroyed independently of the `pod` lifecycle. -->

<br />

## **Basic** `Commands` 📝

* **get** `pvcs`

    ```shell
    kubectl get pvc
    ```

* **delete** `pvcs`

    ```shell
    kubectl delete pvc <pvc-name>
    ```

  * but what happens to the underlying `persistent volume` 🤔
    * by default the `persistent volume` reclaim policy is set to `retain`, but can be changed to `delete` or `recycle`.

        ```yaml
            # persistent volume reclaim policy can be set to delete, retain, or recycle
            # this is placed in the pv spec section
            persistentVolumeReclaimPolicy: Retain
        ```

<br />

## **Examples** 🧩

* `persistent volume claim` definition

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
        name: myclaim
    spec:
        accessModes:
        - ReadWriteOnce
        resources:
            requests:
                storage: 500Mi
    ```

  * similar to persistent volumes, **accessMode** can be `ReadWriteOnce`, `ReadOnlyMany`, or `ReadWriteMany`

* use `persistent volume claim` in a `pod` definition

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: mypod
    spec:
        containers:
          - name: myfrontend
            image: nginx
            volumeMounts:
              - mountPath: "/var/www/html"
                name: mypd
        volumes:
          - name: mypd
            persistentVolumeClaim:
                claimName: myclaim
    ```

  * `persistent volume claim` is defined in the `volumes` section of the `pod` definition
  * `persistent volume claim` is mounted to the `pod` in the `volumeMounts` section of the `pod` definition

* `pvc` for use with examples in ***pv*** and ***volumes*** section

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
        name: claim-log-1
    spec:
        accessModes:
          - ReadWriteOnce
        resources:
            requests:
            storage: 50Mi
    ```

  * update pod to use `pvc`

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: webapp
    spec:
        containers:
            - name: event-simulator
            image: kodekloud/event-simulator
            env:
              - name: LOG_HANDLERS
                value: file
            volumeMounts:
              - mountPath: /log
                name: log-volume
        volumes:
          - name: log-volume
            persistentVolumeClaim:
                claimName: claim-log-1
    ```

<br />

[↩️](../README.md)
