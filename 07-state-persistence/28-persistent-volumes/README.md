# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Persistent Volumes*** 🏰

## **Description** 👀

`Persistent Volumes` are a way to *store data* in a `pod` that will persist even if the `pod` is destroyed. `Persistent Volumes` are also a way to *share data* between `pods`. `Persistent Volumes` are a resource that is independent of the `pod` lifecycle. This means that `Persistent Volumes` can be created, used, and destroyed independently of the `pod` lifecycle.

<!-- <br />

## **Basic** `Commands` 📝

<br /> -->

## **Examples** 🧩

* `persistent volume` definition

    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
        name: pv-vol1
    spec:
        # access mode defines how the volume should be mounted on the host
        accessModes:
          - ReadWriteOnce
        capacity:
            storage: 1Gi
        # host path is the path on the host where the volume will be mounted, there are other types of volumes
        hostPath:
            path: /tmp/dat
    ```

* `pv` to be added on in *later section*

  ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: pv-log
  spec:
    accessModes:
      - ReadWriteOnce
    capacity:
      storage: 100Mi
    hostPath:
      path: /pv/log
  ```

  * supported access modes are
    * **ReadOnlyMany**
    * **ReadWriteMany**
    * **ReadWriteOnce**

<br />

[↩️](../README.md)
