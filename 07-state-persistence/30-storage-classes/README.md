# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Storage Classes*** 📦


## **Description** 👀

With `Storage Classes` you can define a provisioner that can automatically provision storage and attach that to `pods`. 


<br />

## **Basic** `Commands` 📝

<br />


## **Examples** 🧩


* `storage class` definitions

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
        name: google-storage
    provisioner: kubernetes.io/gce-pd
    ```

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
        name: aws-ebs
    provisioner: kubernetes.io/aws-ebs
    ```

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata: 
    name: delayed-volume-sc
    provisioner: kubernetes.io/no-provisioner
    volumeBindingMode: WaitForFirstConsumer
    ```


  * `provisioner` is the name of the `storage provisioner` that will be used to provision the `persistent volume`
  * `parameters` are the parameters that will be passed to the `storage provisioner`

  * for `pvc` to use the `storage class`, specify the `storage class` name in pvc `spec.storageClassName` field

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
        name: myclaim
    spec:
        storageClassName: google-storage
        accessModes:
            - ReadWriteOnce
        resources:
            requests:
                storage: 500Mi
    ```

<br />

[↩️](../README.md)
