# **Kubernetes** - ***Secrets***

<br>

`Secrets` are used to store *sensitive information* such as `passwords`, `API keys`, and `ssh keys`. Secrets are stored in the cluster as *base64 encoded strings*. Secrets can be create using the `kubectl` command or using a `Secret` manifest file.

* A `secret` is only sent to a `node` if a `pod` on that `node` requires it.

* `Kubelet` stores the `secret` into a tmpfs so that the `secret` is *not written to disk storage*.

* Once the `Pod` that depends on the `secret` is **deleted**, `kubelet` will **delete** its *local copy* of the secret data as well.

<br>

`Secrets` are *not encrypted*, so it is ***not safer*** in that sense. However, s*ome best practices around* using `secrets` make it ***safer***. As in best practices like:

* Not checking-in secret object definition files to source code repositories.

* **[Enabling Encryption at Rest](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)** for Secrets so they are stored encrypted in `ETCD`.

<br>

Read about the protections and risks of using secrets **[here](https://kubernetes.io/docs/concepts/configuration/secret/#protections)**.

<br>

## ***Basic*** `Commands` 📝

<br>

* **create** **`secrets`** using the `kubectl` command

    ```bash
    kubectl create secret generic <secret name> --from-literal=<key>=<value>
    ```

* **create** **`secrets`** using a `manifest file`

    ```bash
    kubectl create secret generic <secret name> --from-file=<path to file>
    ```

* **get** **`secrets`**

    ```bash
    kubectl get secret <secret name>
    ```

* **get** all **`secrets`**

    ```bash
    kubectl get secrets
    ```

* **describe** **`secrets`**

    ```bash
    kubectl describe secret <secret name>
    ```

  * note that this method ***does not show the secret value***

<br>

* **view** **`secrets`** *and their values*

    ```bash
    kubectl get secret <secret-name> -o yaml
    ```

* **delete** **`secrets`**

    ```bash
    kubectl delete secret <secret-name>
    ```

<br>

## **Examples** 📚

<br>

* command used for:&nbsp; `secret-examples/sample-secret.yaml`

    ```bash
    kubectl create secret generic sample-secret --from-file=secret-examples/DB_Host --from-file=secret-examples/DB_User --from-file=secret-examples/DB_Password 
    ```

* command used for:&nbsp; `secret-examples/sample-secret2.yaml`

    ```bash
    kubectl create secret generic sample-secret2 --from-literal=DB_Host=postgres --from-literal=DB_User=guerrero --from-literal=DB_Password=pokemon
    ```

* sample `secrets`

    **`DB_Host`**

    ```bash
    postgres
    ```

    **`DB_User`**
    ```bash
    guerrero
    ```

    **`DB_Password`**

    ```bash
    pokemon
    ```

* sample `secret` manifest file

    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
        creationTimestamp: null
        name: sample-secret
    data:
        DB_Host: cG9zdGdyZXM=
        DB_Password: cG9rZW1vbg==
        DB_User: Z3VlcnJlcm8=
    ```

* sample `pod` with `secret` manifest file

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: secret-pod
    spec:
        containers:
          - name: secret-container
            image: nginx
            ports:
              - containerPort: 80
            envFrom:
              - secretRef:
                name: sample-secret
    ```