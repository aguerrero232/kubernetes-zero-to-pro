# Kubernetes - ***Secrets***

<br>

Secrets are used to store **sensitive information** such as `passwords`, `API keys`, and `ssh keys`. Secrets are stored in the cluster as **base64 encoded strings**. Secrets can be create using the `kubectl` command or using a **Secret** manifest file.

* A secret is only sent to a node if a pod on that node requires it.

* Kubelet stores the secret into a tmpfs so that the secret is not written to disk storage.

* Once the Pod that depends on the secret is deleted, kubelet will delete its local copy of the secret data as well.

<br>

Secrets are not encrypted, so it is not safer in that sense. However, some best practices around using secrets make it safer. As in best practices like:

* Not checking-in secret object definition files to source code repositories.

* **[Enabling Encryption at Rest](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)** for Secrets so they are stored encrypted in ETCD. 

<br>



Read about the protections and risks of using secrets **[here](https://kubernetes.io/docs/concepts/configuration/secret/#protections)**.

<br>

___

<br>

## **Basic Commands**

* to create **secrets** using the `kubectl` command, you can use the following command:

    ```
        kubectl create secret generic <secret name> --from-literal=<key>=<value>
    ```

* to create **secrets** using a `manifest file`, you can use the following command:

    ```
        kubectl create secret generic <secret name> --from-file=<path to file>
    ```

* to get **secrets** you can use the following command:

    ```
        kubectl get secret <secret name>
    ```

* to get all **secrets** you can use the following command:

    ```
        kubectl get secrets
    ```

* to describe **secrets** you can use the following command:

    ```
        kubectl describe secret <secret name>
    ```
    * note that this method does not show the secret value

* to view **secrets** and their values you can use the following command:

    ```
        kubectl get secret <secret name> -o yaml
    ```

* to delete **secrets** you can use the following command:

    ```
        kubectl delete secret <secret name>
    ```

<br>

___ 

<br>

## **Examples**

<br>

* command used for:&nbsp; `secret-examples/sample-secret.yaml`

    ```
    kubectl create secret generic sample-secret --from-file=secret-examples/DB_Host --from-file=secret-examples/DB_User --from-file=secret-examples/DB_Password 
    ```

* command used for:&nbsp; `secret-examples/sample-secret2.yaml`

    ```
    kubectl create secret generic sample-secret2 --from-literal=DB_Host=postgres --from-literal=DB_User=guerrero --from-literal=DB_Password=pokemon
    ```


<br>