# **Kubernetes** - ***Montior*** *and* ***Debug Applications*** 🕸️

`Kubernetes` runs an agent on each `node` known as a `kubelet`. The `kubelet` is responsible for ensuring that the containers are running in a pod. The `kubelet` also exposes a `/metrics/cadvisor` endpoint that provides metrics about the `node` and its containers. The `kubelet` uses cAdvisor to collect these metrics. *cAdvisor* is an open source project that collects resource usage and performance metrics about running containers. *cAdvisor* is built into the `kubelet` binary and is available at the `/metrics/cadvisor` endpoint on the `kubelet`.

<br />

## ***Metrics Server*** 📊

The `metrics server` is a *cluster-wide aggregator* of resource usage **data**. The `metrics server` collects resource metrics from *all* `nodes` in the cluster, aggregates the **data**, and exposes the metrics via an `API`. The `metrics server` is not enabled by default in Kubernetes. To enable the `metrics server`, *you must install* the `metrics server`.

* `minikube` **install**

    ```bash
    minikube addons enable metrics-server
    ```

* **other**

    ```bash
    git clone https://github.com/kubernetes-incubator/metrics-serve
    ```

    ```bash
    kubectl create -f deploy/1.8+/
    ```

<br />

## **Basic** `Commands` 📝


* **view** the *metrics* for the *top performing* `nodes`

    ```bash
    kubectl top nodes
    ```

* **view** the *metrics* for the *top performing* `nodes` in a `namespace`

    ```bash
    kubectl top nodes -n <namespace>
    ```

* **view** the `node` that *consumes the most* memory

    ```bash
    kubectl top node --sort-by='memory' --no-headers | head -1 
    ```

* **view** the `node` that *consumes the least* ***memory***

    ```bash
    kubectl top node --sort-by='memory' --no-headers | tail -1
    ```

* **view** the `node` that *consumes the most* ***cpu***

    ```bash
    kubectl top node --sort-by='cpu' --no-headers | head -1 
    ```

* **view** the `node` that *consumes the most* ***cpu***

    ```bash
    kubectl top node --sort-by='cpu' --no-headers | tail -1 
    ```


* **view** the *metrics* for the *top performing* `pods`

    ```bash
    kubectl top pods
    ```

* **view** the *metrics* for the *top performing* `pods` in a `namespace`

    ```bash
    kubectl top pods -n <namespace>
    ```

* **view** the `pod` that *consumes the most* ***memory***

    ```bash
    kubectl top pod --sort-by='memory' --no-headers | head -1 
    ```

* **view** the `pod` that *consumes the least* ***memory***

    ```bash
    kubectl top pod --sort-by='memory' --no-headers | tail -1
    ```

* **view** the `pod` that *consumes the most* ***cpu***

    ```bash
    kubectl top pod --sort-by='cpu' --no-headers | head -1 
    ```

* **view** the `pod` that *consumes the most* ***cpu***

    ```bash
    kubectl top pod --sort-by='cpu' --no-headers | tail -1 
    ```

<br>

[↩️ **back**](../)
