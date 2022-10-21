# Kubernetes - **Taints and Tolerations**

`Taints` and `Tolerations` are features that allow you to control the placement of pods on nodes. Taints are applied to nodes, and tolerations are applied to pods.A `taint` on a `node` ***instructs*** the `node` to ***repel all*** `pods` that do not `tolerate` the `taint`.

___

<br >

## **Basic Commands**

### ***Taints - Node***

* generic

  ```shell
  kubectl taint nodes <node-name> <key>=<value>:<taint-effect>
  ```

  **taint-effect**: `NoSchedule`, `PreferNoSchedule`, `NoExecute`

* example

  ```shell
  kubectl taint nodes node1 app=blue:NoSchedule
  ```

* to see if taints exist on a node

  ```shell
  kubectl describe node node01 | grep taint
  ```

### ***Tolerations - Pod***

```yaml
spec:
  tolerations:
    - key: app
      operator: "Equal"
      value: blue
      effect: NoSchedule
```


## Bee and Mosquito Example

create node01

```yaml
apiVersion: v1
kind: Node
metadata:
  name: node01
spec:
```

```yaml
apiVersion: v1
kind: Node
metadata:
  name: controlplane
  # add a taint with key spray and value mortien and effect NoSchedule
  taint: 
    - key: spray
      value: mortien
      effect: NoSchedule
spec:


```


* apply taint

kubectl taint nodes node01 spray=mortein:NoSchedule


* create the bee and mosquito pods and watch what happens
  * bee will be scheduled on node01 and mosquito will not be scheduled on any node

* remove the taint on controlplane
  * mosquito will be scheduled on controlplane
