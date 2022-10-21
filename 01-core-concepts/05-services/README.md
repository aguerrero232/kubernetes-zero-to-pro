# **Kubernetes** - ***Services***

A `service` is a way to expose an application running on a set of `pods` as a `network service`. It is `services` that enables connectivity between `pods` and *external clients*.

<br>

## ***Types*** *of* `Services`


* `NodePort`
  * makes an **internal port** accessible on the `node`
  * uses three **ports**
  * one *port* on the `node`, the `node port`
    * the `node` ports *range* is *between* ***30000-32767***
  * one *port* on the `pod`, the `target port`
  * one *port* on the `service`, the `service port`

* `ClusterIP`
  * **creates** a **virtual IP** inside the `cluster` that allows other `pods` to *communicate with it*
  * helps *provide a single interface* to a set of pods

* `LoadBalancer`
  * *provisions* a `load balancer`
  * only works on cloud providers that support native` load balancers`

<br>

## ***Basic*** `Commands`

<br>

* **create** a `service`

```shell
kubectl create -f  <yaml-file>
```

* **get** list of `services`

```shell
kubectl get services
```

* **get** *descriptive information* on the desired `service`

```shell
kubectl describe service <service-name>
```

* **access** `service` *in browser running* on `minikube`

```shell
minikube service <service-name> --url
```
