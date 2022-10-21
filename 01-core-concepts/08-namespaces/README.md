# **Kubernetes** `-` ***Namespaces***

`Namespaces` provides a mechanism for isolating groups of resources within a single cluster.

* Names of resources need to be **unique within a namespace**, but **not across namespaces**.
* Intended **for use in environments with many users** spread across multiple teams, or projects.
* Can be used to set a resource quota

<br />

## ***Basic*** `Commands`

<br />

* **list** *current* `namespaces`

```shell
kubectl get namespace
```

* **create** a `namespace`

```shell
kubectl create namespace <namespace-name>
```

* **delete** a `namespace`

```shell
kubectl delete namespace <namespace-name>
```

* **get** *all resources in* a `namespace`

```shell
kubectl get all --namespace <namespace-name>
```
