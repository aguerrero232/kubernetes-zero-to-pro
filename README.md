# Kubernetes Zero To Pro ✨

<img src="assets/img/k8-header.png" width="100%" height="330px">

<br/>

### ⛏️ ***"A stone is broken by the last stroke of the hammer. This does not mean that the first stroke was useless. Success is the result of continuous effort."*** ⛏️

<br>

## ***Table*** *of* ***`Contents`*** 📜

0. 🗃️ [***resources***](00-resources/README.md)
1. 🧠 [***core concepts***](01-core-concepts/README.md)
   * 🐋 [***pods***](01-core-concepts/01-pods/README.md)
   * 👯 [***replica sets*** *and* ***replication controllers***](01-core-concepts/02-replica-sets/README.md)
   * 🚀 [***deployments***](01-core-concepts/03-deployments/README.md)
   * 🖧 [***networking***](01-core-concepts/04-networking/README.md)
   * 🛎️ [***services***](01-core-concepts/05-services/README.md)
   * 🏗️ [***microservice architecture***](01-core-concepts/06-microservices-architecture/README.md)
   * ☁️ [***cloud***](01-core-concepts/07-kubernetes-on-cloud/README.md)
   * 📛 [***namespaces***](01-core-concepts/08-namespaces/README.md)
   * 🧙 [***imperative commands***](01-core-concepts/09-imperative-commands/README.md)
2. ⚙️ [***configuration***](02-configuration/README.md)
   * 🔣 [***container arguments***](02-configuration/10-commands-and-arguments/README.md)
   * 🗺️ [***configmaps***](02-configuration/11-config-maps/README.md)
   * 🕵️ [***secrets***](02-configuration/12-secrets/README.md)
   * 💁 [***service accounts***](02-configuration/13-service-accounts/README.md)
   * 💾 [***resource requirements***](02-configuration/14-resource-requirements/README.md)
   * ☢️ [***taints*** *and* ***tolerations***](02-configuration/15-taints-and-tolerants/README.md)
   * 🔘 [***node selectors*** *and* ***affinity***](02-configuration/16-node-selectors-and-affinity/README.md)
3. 🐳<sup>🐳</sup> [***multi-container pods***](03-multi-container-pods/README.md)
   * 🐳<sup>🐳</sup> [***multi-container pods***](03-multi-container-pods/17-multi-container-pods/README.md)
   * 💥 [***init containers***](03-multi-container-pods/18-init-containers/README.md)
4. 🔬 [***observability***](04-observability/README.md)
   * 🛸 [***readiness*** *and* ***liveness probes***](04-observability/19-readiness-and-liveness-probes/README.md)
   * 📄 [***container logging***](04-observability/20-container-logging/README.md)
   * 🕸️ [***monitor*** *and* ***debug apps***](04-observability/21-monitor-and-debug-apps/README.md)
5. 💠 [***pod design***](05-pod-design/README.md)
   * 🏷️ [***labels selectors*** *and* ***annotations***](05-pod-design/22-labels-selectors-annotations/README.md)
   * 👔 [***jobs***](05-pod-design/23-jobs/README.md)
   * ⏳ [***cron jobs***](05-pod-design/24-cron-jobs/README.md)
6. 🤯 [***advanced services*** *and* ***networking***](06-adv-services-and-networking/README.md)
   * ⚖️ [***ingress networking***](06-adv-services-and-networking/25-ingress-networking/README.md)
   * 🤝 [***network policies***](06-adv-services-and-networking/26-network-policies/README.md)
7. 🗄️ [***state persistence***](07-state-persistence/README.md)
   * 💾 [***volumes***](07-state-persistence/27-volumes/README.md)
   * 🏰 [***persistent volumes***](07-state-persistence/28-persistent-volumes/README.md)
   * 🚩 [***persistent volume claims***](07-state-persistence/29-persistent-volume-claims/README.md)
   * 📦 [***storage classes***](07-state-persistence/30-storage-classes/README.md)
   * 🌟 [***stateful sets***](07-state-persistence/31-stateful-sets/README.md)
   * 🧟 [***headless service***](07-state-persistence/32-headless-service/README.md)

<br />

## ***Kubernetes*** `Architecture` 🏗️

***Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.***

<br>

<img src="assets/img/clusterdiagram2.PNG" width="615px"> <img src="assets/img/clusterdiagram-legend.PNG" width="150px">

* The **`Control Plane`** is responsible for *managing the cluster*.

  * **Components**

    * `kube-apiserver` - Exposes the `Kubernetes API`
    * `etcd` - *Consistent and highly-available key value store* used as Kubernetes' backing store for all cluster data.
    * `kube-scheduler` - Watches for newly created `Pods` with no assigned `node`, and selects a `node` for them to run on.
    * `kube-controller-manager` - Runs `controller` processes. Each `controller` is a separate process but to keep things simple they are compiled together and run in a single process
      * Examples
        * `Node controller`: Responsible for noticing and responding when `nodes` go down.
        * `Job controller`: Watches for Job objects that represent one-off tasks, then creates `Pods` to run those tasks to **completion**.
        * `Endpoints controller`: Populates the Endpoints object (that is, joins Services & Pods).
        * `Service Account` & `Token controllers`: Create default accounts and `API` *access tokens* for new `namespaces`

    * `cloud-controller-manager` - Embeds cloud-specific control logic
      * `Node`, `Route`, and `Service controllers` can have cloud provider dependencies.

<br/>

* A `Node` is a `VM` or a *physical computer* that serves as a *worker machine* in a `Kubernetes` cluster.
  * The `nodes` communicate with the control plane using the `Kubernetes API`

  * **Components**
    * `kubelet` - An agent that runs on each node in the cluster. It makes sure that `containers` are running in a `Pod`.
      * `kube-proxy` - Network proxy that runs on each `node` in your cluster, implementing part of the *`Kubernetes` Service concept*.
    * `Container runtime` - **Software** that is *responsible for running* `containers`.

<br>

## **Basic** `Commands` 📝

* ## `kubectl` **commands** <img src="assets/img/k8s.png" width="24px">

  * **check** version of `Kubernetes` being used

    ```bash
    kubectl version
    ```

  * **get** *everything*

    ```bash
    kubectl get all
    ```

  * **get** api `resources` includes *name*, *shortnames*, *api version*, if *namespaced*, and *kind*

    ```bash
    kubectl api-resources
    ```

  * **get** kube-api `version`

    ```bash
    kubectl api-versions
    ```

  * all resources in kubernetes are grouped into `API groups`
    * under each `API group` are `API resources`

      ```bash
      kubectl api-resources
      ```

      * `API resources` are the *objects* that can be have **verbs** act on them from the `Kubernetes API`
        * ***verbs***: `create`, `get`, `describe`, `delete`, `update`, `watch`, `list`

  * identify `kube-apiserver` settings

    ```bash
    kubectl describe pod kube-apiserver-controlplane -n kube-system
    ```

* ## `minikube` **commands** <img src="assets/img/minikube.png" width="24px">

  * Check the status of `minikube`

    ```bash
    minikube status
    ```

  * *start* `minikube`

    ```bash
    minikube start
    ```

  * **stop** `minikube`

    ```bash
    minikube stop
    ```
