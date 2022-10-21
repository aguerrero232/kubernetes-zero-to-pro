# **Kubernetes** `-` ***Imperative Commands***

`Imperative commands` can help in getting one time tasks done quickly, as well as ***generate a definition template easily***.

<br />

**Familiarize yourself with the following commands**

* `--dry-run`
  * will execute, and the resource **will be created**.

* `--dry-run=client`
  * will execute, but the resource **will not be created**.

* `-o yaml`
  * will **output the resource definition** in `yaml` format.


<br>

## ***Basic*** `Commands`

<br>

use *in combination* to ***generate a resource definition file quickly***, that you can *then modify and create resources as required*, **instead of creating the files from scratch**.


<br>

* **create** a `pod` manifest file

    ```shell
    kubectl run <pod-name> --image=<image-name> --dry-run=client -o yaml
    ```

* **create** a `deployment` manifest file

    ```shell
    kubectl create deployment --image=<image-name> --dry-run=client -o yaml
    ```

* **create** a `service` manifest file

    ```shell
    kubectl expose <object-type> <object-name> --port=<port> --name <service-name> --dry-run=client -o yaml
    ```

# **Examples**

<br />

* **create** a `service` named nginx of type `NodePort` to expose `pod` nginx's *port 80* on *port 30080* on the `nodes`

    ```shell
    kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
    ```

    (This will **automatically** use the *pod's labels as selectors*, but you **cannot** specify the `node port`. You have to *generate a definition file* and then add the `node port` in manually before creating the service with the `pod`.)
    
    <br />

* **deploy** a *redis* `pod` using the *redis:alpine image* with the *labels* set to **tier=db**.

    ```shell
    kubectl run redis --image=redis:alpine --labels="tier=db" --dry-run=client -o yaml > redis-pod.yaml
    ```

  * **output**

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        tier: db
    name: redis
    spec:
    containers:
    - image: redis:alpine
        name: redis
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Always
    status: {}
    ```

* **create** a `service` *redis-service* to expose the *redis* application within the cluster on *port 6379*

    ```shell
    kubectl expose pod redis --port=6379 --name=redis-service --type=ClusterIP --dry-run=client -o yaml > redis-service.yaml 
    ```

* **create** a `deployment` named *webapp* using the image *kodekloud/webapp-color* with three *replicas*

    ```shell
    kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3 --dry-run=client -o yaml > webapp-dep.yaml
    ```

* **create** a `pod` using *nginx* with `container` port *8080 exposed*

    ```shell
    kubectl run custom-nginx --image=nginx --port=8080
    ```

* **create** a new `deployment` called *redis-deploy* in the *dev-ns namespace* with the *redis image*, it should have two *replicas*

    ```shell
    kubectl -n dev-ns create deployment redis-deploy --image=redis --replicas=2 --dry-run=client -o yaml > rd-dev.yaml
    ```
