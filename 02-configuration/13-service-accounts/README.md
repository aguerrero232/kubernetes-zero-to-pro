# **Kubernetes** - ***Service Accounts***


**`kubernetes` documents reference** - ***[Service Accounts](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)***

<br>

When a `pod` is **created** it automatically links it to a `service account`. 

<br>

## ***Basic*** `Commands` 📝

<br>


* create a new service account
  ```bash
  kubectl create serviceaccount <account-name>
  ```

## **Examples** 📚

<br>

* sample `service account` manifest file
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: RoleBinding
  metadata:
    name: read-pods
    namespace: default
  subjects:
  - kind: ServiceAccount
    name: dashboard-sa # Name is case sensitive
    namespace: default
  roleRef:
    kind: Role #this must be Role or ClusterRole
    name: pod-reader # this must match the name of the Role or ClusterRole you wish to bind to
    apiGroup: rbac.authorization.k8s.io
  ```