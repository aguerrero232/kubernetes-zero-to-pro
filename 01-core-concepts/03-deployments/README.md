# **Kubernetes** - ***Deployments***

`Deployments` are the preferred way to manage pods. They are a **higher level abstraction** than` Replica Sets`. They allow you to *define the desired state* of your application, and the `controller` will make sure that the current state matches the desired state. 

<br>

## ***Updates*** *and* ***Rollbacks***

<br>

* `Deployments` allow you to **`update` your application without downtime**.

* There are **two methods** to `update` your application:

  * **`Rolling Update`** - The new version of the application is *deployed* in stages. The old version is still running while the new version is being *deployed*. Once the new version is *deployed*, the old version is *terminated*.

  * **`Recreate`** - The old version of the application is terminated *before* the new version is *deployed*.

* `rollbacks` are also possible. You can `rollback` to a *previous version* of your application.

<br>

## ***Basic*** `Commands`

<br>

* **create** a new deployment

  ```shell
  kubectl create -f <yaml-file>
  ```

* **update** a `deployment` &nbsp; (`rolling update`)

  ```shell
  kubectl apply -f <yaml-file>
  ```

  ```shell
  kubectl set image deployment/<deployment-name> <new-image>
  ```

* **get** list of `deployments`

  ```shell
  kubectl get deployments
  ```

* **get** *descriptive information* on the desired `deployment`

  ```shell
  kubectl describe deployment <deployment-name>
  ```

* **get** the *rollout status* of the `deployment`

  ```shell
  kubectl rollout status deployment/<deployment-name>
  ```

* **get** the *rollout history* of the `deployment`

  ```shell
  kubectl rollout history deployment/<deployment-name>
  ```

* **rollback** to a *previous version* of the `deployment`

  ```shell
  kubectl rollout undo deployment/<deployment-name>
  ```

* ***use*** the `--to-revision` flag to *specify* the `revision number` to **rollback** to.

  ```shell
  kubectl rollout undo deployment/<deployment-name> --to-revision=<revision-number>
  ```

* **view** `deployment` at a specific `revision`

  ```shell
  kubectl rollout history deployment <deployment-name> --revision=<revision-number>
  ```

* **use** the `--record` flag to *save the command used* to **create/update** a `deployment`

  ```shell
  kubectl apply -f <yaml-file> --record=true
  ```


