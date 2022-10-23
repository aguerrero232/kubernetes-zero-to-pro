# **Kubernetes** - **Replication Controllers** *and* ***Replica Sets*** 👯

`Replica Sets` are **newer** than `Replication Controllers`, and are the ***preferred way*** to manage `pods`!

<br />

**Examples of simple Replication Controller and Replica set are defined in the yaml files included in this directory**

<br />

A `Replica Set` is a *set of* `pods` that are **managed** by a `controller`. It **ensures** that the *specified number of pods* are running at any given time. If a pod fails, the `Replica Set` will **create** a new one to *replace it*.

<br />

## **Why** use `Replica Sets` 💭

They *enable* users to **monitor** `pods`, by labeling `pods` it will allow `replica set` to know which `pods` to monitor and provides a method to **filter** out `pods` thats are not part of the `replica set`.

<br />

## ***Basic*** `Commands` 📝

* **create** a `replica set`

```bash
kubectl create -f <yaml-file>
```

* **get** list of `replica sets`

```bash
kubectl get replicaset
```

* **get** *descriptive information* on the desired `replica set`

```bash
kubectl describe replicaset <replica-set-name>
```

* **edit** the specified `replica set`

```bash
kubectl edit replicaset <replica-set-name>
```

* **scale** `replica set` to the *desired number* of `replicas`

```bash
kubectl replace -f <edited-yaml-file>
```

```bash
kubectl scale --replicas=<new-number-of-replicas> -f <yaml-file>
```

* **delete** specified `replica set`

```bash
kubectl delete replicaset <replica-set-name>
```

<br />

## **Examples** 🧩

* sample `replication controller` definition

    ```yaml
    apiVersion: v1
    kind: ReplicationController
    metadata:
        name: myapp-rc
        labels:
            app: myapp
            type: front-end
    # most crucial for replication controller
    spec:
        template:
            # pod template for the replication controller
            metadata:
                name: myapp-pod
                labels:
                    app: myapp
                    type: front-end
            spec:
                containers:
                  - name: nginx-container
                    image: nginx
        replicas: 3
    ```

* sample `replica set` definition

    ```yaml
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
        name: myapp-rs
        labels:
            app: myapp
            type: front-end
    spec: 
        template:
            metadata:
                name: myapp-pod
                labels:
                    app: myapp
                    type: front-end
            spec:
                containers:
                  - name: nginx-container
                    image: nginx
        replicas: 3
        #  one of the major differences between replica controller and replica set
        selector: 
            matchLabels:
            type: front-end
    ```

<br>

[↩️ **back**](../)
