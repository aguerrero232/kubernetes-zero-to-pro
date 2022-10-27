# <img src="../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Section 2:*** `Configuration` ⚙️

## ***Table*** *of* ***`Contents`*** 📜

* 🏠 [**home**](https://github.com/aguerrero232/kubernetes-zero-to-pro/blob/main/README.md)
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
