# Kubernetes Zero To Pro ✨

## ***Table*** *of* ***`Contents`*** 📜

* 🗃️ [***resources***](00-resources/)
* 🧠 [***core concepts***](01-core-concepts/)
* ⚙️ [***configuration***](02-configuration/)
* 🐳<sup>🐳</sup> [***multi-container pods***](03-multi-container-pods/) 
* 🔬 [***observability***](04-observability/)
* 💠 [***pod design***](05-pod-design/)


<br />

## ***Kubernetes*** `Architecture` 🏗️

<br>

***Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.***

<br>

![](00-resources/img/clusterdiagram2.PNG) ![](00-resources/img/clusterdiagram-legend.PNG)

<br/>

* The **`Control Plane`** is responsible for *managing the cluster*.

  * **Components**

    * `kube-apiserver` - Exposes the `Kubernetes API`
    * `etcd` - *Consistent and highly-available key value store* used as Kubernetes' backing store for all cluster data.
    * `kube-scheduler` - Watches for newly created `Pods` with no assigned `node`, and selects a `node` for them to run on.
    * `kube-controller-manager` - Runs `controller` processes. Each `controller` is a separate process but to keep things simple they are compiled together and run in a single process
      * Examples 📚
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

## ***Basic*** `Commands` 📝


* ## `minikube` **commands** <img src="00-resources/img/minikube.png" width="24px">

  * Check the status of minikube

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

<br>

* ## `kubectl` **commands** <img src="00-resources/img/k8s.png" width="24px">

  * **check** version of `kubernetes` being used

    ```bash
    kubectl version
    ```

  * **get** *everything*

    ```bash
    kubectl get all
    ```

<br>

* ## `usefull` **commands** ⚡

  * **view** the flavor and **version** of `OS`

    ```bash
    cat /etc/os-release
    ```

<br>

# ***YAML***  <img src="00-resources/img/yaml.png" width="29px">

<br />

`YAML` is a ***human-readable data serialization language***. It is commonly used for *configuration files* and in applications where data is being stored or transmitted. `YAML` is stored in **key value pairs** and can be used to serialize data structures such as *maps, sequences, and scalars*.

<br>

## `YAML` **Syntax**

* `YAML` is case sensitive
* Comments are created using the # symbol

<br>

## **Examples** 📚

* key value pairs

  ```yaml
  Fruit: Apple
  Vegetable: Carrot
  Liquid: Water
  Meat: Chicken
  ```

* arrays / lists

  ```yaml
  Fruits:
    - Orange
    - Apple
    - Banana

  Vegetables:
    - Carrot 
    - Cauliflower
    - Tomato
  ```

* dictionary / map

  ```yaml
  Banana:
      Calories: 105
      Fat: 0.4g
      Carbs: 27g

  Grapes:
      Calories: 62
      Fat: 0.3g
      Carbs: 16g
  ```

* key value / dictonary / lists

  ```yaml
  Fruits:
    - Banana:
        Calories: 105
        Fat: 0.4g
        Carbs: 27g

    - Grapes:
        Calories: 62
        Fat: 0.3g
        Carbs: 16g
  ```

***Notice the alignment, this is important in yaml.***

* You can *either* set a value or a list/dictonary/map but *not both*

* `Dictionaries` are an *unordered collection* while `lists` are *ordered*
