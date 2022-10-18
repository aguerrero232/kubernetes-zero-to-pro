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

### ***Tolerations - Pod***

```yaml
spec:
  tolerations:
    - key: app
      operator: "Equal"
      value: blue
      effect: NoSchedule
```
