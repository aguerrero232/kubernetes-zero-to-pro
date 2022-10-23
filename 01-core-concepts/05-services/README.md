# **Kubernetes** - ***Services*** 🛎️

A `service` is a way to expose an application running on a set of `pods` as a `network service`. It is `services` that enables connectivity between `pods` and *external clients*.

<br>

## ***Types*** *of* `Services` 🟦🟩🟪

* `NodePort`
  * makes an **internal port** accessible on the `node`
  * uses three **ports**
  * one *port* on the `node`, the `node port`
    * the `node` ports *range* is *between* ***30000-32767***
  * one *port* on the `pod`, the `target port`
  * one *port* on the `service`, the `service port`

* `ClusterIP`
  * **creates** a **virtual IP** inside the `cluster` that allows other `services` to *communicate with it*
  * helps *provide a single interface* to a set of pods

* `LoadBalancer`
  * *provisions* a `load balancer`
    * only works on cloud providers that support native `load balancers`

## **More** on `ClusterIP` ✨

`CusterIP` is used to *expose* a `service` to other `pods` in the `cluster`. It provides a *single*  interface that other `pods` can use to *access* the `service`. This *enables the ability* to easily and efficiently *scale* the `service` by adding or removing `pods` as needed.

<br>

## ***Basic*** `Commands` 📝

* **create** a `service`

```bash
kubectl create -f  <yaml-file>
```

* **get** list of `services`

```bash
kubectl get services
```

* **get** *descriptive information* on the desired `service`

```bash
kubectl describe service <service-name>
```

* **access** `service` *in browser running* on `minikube`

```bash
minikube service <service-name> --url
```

<br>

## ***Creating*** *a* `Service` 🛠️

* basic `service` definition

  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: webapp-service
  spec:
    type: NodePort
    ports:
      # only port is needed, other fields are optional 
      - targetPort: 8080
        port: 8080 # port on the service object
        nodePort: 30080 
    # selector is used to find the pods to route traffic to
    selector:
      name: simple-webapp
  ```

  what do you do when you have multiple `pods`?

  when the `service` is created, it will *select* all `pods` that match the `selector` and *route traffic* to them. No additional configuration is needed. 🌟 ***It's magic.*** 🌟

<br />

## **Examples** 📚

* sample `NodePort service` definition

  ```yaml
  apiVersion: v1 
  kind: Service
  metadata:
    name: myapp-service
  spec:
    type: NodePort
    ports:
      - targetPort: 80
        port: 80
        nodePort: 30008
    selector:
      app: myapp
      type: front-end
  ```

* sample `ClusterIP service` definition

  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: back-end
  spec:
    type: ClusterIP
    ports:
      - targetPort: 80
        port: 80
    selector:
      app: myapp
      type: back-end
  ```

<br>

↩️ [**back**](../)
