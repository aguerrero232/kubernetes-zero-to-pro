# **Kubernetes** - ***Montior*** *and* ***Debug Applications***

`Kubernetes` runs an agent on each `node` known as a `kubelet`. The `kubelet` is responsible for ensuring that the containers are running in a pod. The `kubelet` also exposes a `/metrics/cadvisor` endpoint that provides metrics about the `node` and its containers. The `kubelet` uses cAdvisor to collect these metrics. *cAdvisor* is an open source project that collects resource usage and performance metrics about running containers. *cAdvisor* is built into the `kubelet` binary and is available at the `/metrics/cadvisor` endpoint on the `kubelet`.

## ***Metrics Server***

The `metrics server` is a *cluster-wide aggregator* of resource usage **data**. The `metrics server` collects resource metrics from *all* `nodes` in the cluster, aggregates the **data**, and exposes the metrics via an `API`. The `metrics server` is not enabled by default in Kubernetes. To enable the `metrics server`, *you must install* the `metrics server`.

* `minikube` **install**

    ```shell
    minikube addons enable metrics-server
    ```

* **other**

    ```shell
    git clone https://github.com/kubernetes-incubator/metrics-serve
    ```

    ```shell
    kubectl create -f deploy/1.8+/
    ```


## **Basic** `Commands`**:** `metrics server`

<br />

* **view** the *metrics* for the *top performing* `nodes`

    ```shell
    kubectl top nodes
    ```

* **view** the *metrics* for the *top performing* `nodes` in a `namespace`

    ```shell
    kubectl top nodes -n <namespace>
    ```

* **view** the *metrics* for the *top performing* `pods`

    ```shell
    kubectl top pods
    ```

* **view** the *metrics* for the *top performing* `pods` in a `namespace`

    ```shell
    kubectl top pods -n <namespace>
    ```