# <img src="../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Section 2:*** `Configuration` ⚙️

## ***Table*** *of* ***`Contents`*** 📜

* 🏠 [**home**](../README.md)
* ⚙️ **configuration**
  * 🔣 [**container arguments**](10-commands-and-arguments/README.md)
  * 🗺️ [**configmaps**](11-config-maps/README.md)
  * 🕵️ [**secrets**](12-secrets/README.md)
  * 💁 [**service accounts**](13-service-accounts/README.md)
  * 💾 [**resource requirements**](14-resource-requirements/README.md)
  * ☢️ [**taints** *and* **tolerations**](15-taints-and-tolerants/README.md)
  * 🔘 [**node selectors** *and* **affinity**](16-node-selectors-and-affinity/README.md)
* 🔗 **links**
  * 🔣 [**k8s container arguments documentation**](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/)
  * 🗺️ [**k8s configmaps documentation**](https://kubernetes.io/docs/concepts/configuration/configmap/)
  * 🕵️ [**k8s secrets documentation**](https://kubernetes.io/docs/concepts/configuration/secret/)
  * 💁 [**k8s service accounts documentation**](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)
  * 💾 [**k8s resource requirements documentation**](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
  * ☢️ [**k8s taints** *and* **tolerations documentation**](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
  * 🔘 [**k8s node selectors** *and* **affinity documentation**](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

<br />

## **Description** 👀

***Configuration*** is the process of **setting up your application so that it can run** in a `Kubernetes` cluster.

* Kubernetes does not manage users natively, it relies on external authentication providers.

* **Authentication**
  * Who can access?
    * Files - Username and Password
    * Files - Username and Tokens
    * Certificates
    * External Authentication Providers (LDAP, OAuth, etc.)

* **Authorization**
  * What can they do?
    * RBAC Authorization (Role-Based Access Control)
    * ABAC Authorization (Attribute-Based Access Control)
    * Node Authorization
    * Webhook Authorization

### **Kubeconfig**

`Kubeconfig` is a file that contains the configuration information for `kubectl` to connect to a `Kubernetes` cluster.

* the `Kubeconfig` file has 3 main sections:

  * `clusters` - a list of clusters
    * info about the different clusters that you can connect to
  * `users` - a list of users
    * info about the different users that you can authenticate as
  * `contexts` - a list of contexts
    * info about the different combinations of clusters and users

* `Kubeconfig` definition

    ```yaml
    apiVersion: v1
    kind: Config
    clusters:
      - name: dev
        cluster:
          certificate-authority: /path/to/ca
          server: https://<dev-ip>:6443
    contexts:
      - name: dev@dev
        context:
          cluster: dev
          user: dev
      - name: my-kube-admin@dev
        context:
          cluster: dev
          user: my-kube-admin
    users:
      - name: my-kube-admin
        user:
          client-certificate: /path/to/admin.crt
          client-key: /path/to/admin-key.key
      - name: dev
        user:
          client-certificate: /path/to/dev.crt
          client-key: /path/to/dev-key.key
    ```

  * to change context

    ```bash
    kubectl config use-context <context-name> 
    ```

  * view role bindings

    ```bash
    kubectl get rolebindings --all-namespaces
    ```
  
  * describe role bindings for a specific role
  
    ```bash
    kubectl describe rolebindings <role-name> -n <namespace>
    ```

  * check to see if a user has permissions to a specific resource

    ```bash
    kubectl auth can-i <verb> <resource> -n <namespace>
    ```

  * sample `role`
  
    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: Role
    metadata:
      name: <role-name>
      namespace: <namespace>
    rules:
      - apiGroups: [""] # "" indicates the core API group
        resources: ["pods"]
        verbs: ["get", "watch", "list"]
    ```

  * sample `rolebinding`
  
    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: RoleBinding
    metadata:
      name: <rolebinding-name>
      namespace: <namespace>
    subjects:
    - kind: User
      name: <user-name>
      apiGroup: rbac.authorization.k8s.io
    roleRef:
      kind: Role
      name: <role-name>
      apiGroup: rbac.authorization.k8s.io
    ```

  * `clusterroles` are used to define permissions at the cluster level. (nodes, pvs, etc.)

    * sample `clusterrole`

      ```yaml
      apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRole
      metadata:
        name: <clusterrole-name>
      rules:
        - apiGroups: [""] # "" indicates the core API group
          resources: ["nodes"]
          verbs: ["get", "create", "delete", "list"]
      ```

    * sample `clusterrolebinding`

      ```yaml
      apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRoleBinding
      metadata:
        name: <clusterrolebinding-name>
      subjects:
      - kind: User
        name: <user-name>
        apiGroup: rbac.authorization.k8s.io
      roleRef:
        kind: ClusterRole
        name: <clusterrole-name>
        apiGroup: rbac.authorization.k8s.io
      ```
