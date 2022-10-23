# **Kubernetes** - ***Namespaces*** 📛

`Namespaces` provides a mechanism for isolating groups of resources within a single cluster.

* Names of resources need to be **unique within a namespace**, but **not across namespaces**.
* Intended **for use in environments with many users** spread across multiple teams, or projects.
* Can be used to set a resource quota

<br />

## ***Basic*** `Commands` 📝

* **list** *current* `namespaces`

```bash
kubectl get namespace
```

* **create** a `namespace`

```bash
kubectl create namespace <namespace-name>
```

* **delete** a `namespace`

```bash
kubectl delete namespace <namespace-name>
```

* **get** *all resources in* a `namespace`

```bash
kubectl get all --namespace <namespace-name>
```

<br />

## **Examples** 📚

* sample `namespace` definition

    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
        name: dev
    # defined a rescource quota for the namespace
    spec:
        hard:
            pods: "10"
            requests.cpu: "4"
            requests.memory: 5GI
            limits.cpu: "10"
            limits.memory: 10Gi
    ```

<br>

↩️ [**back**](../)

