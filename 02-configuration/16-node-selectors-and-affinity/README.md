# **Kubernetes** `-` ***Node Selectors*** *and* ***Affinity***


You have **different** types of `workloads` running on your `cluster`, and you want to make sure that the **right** `workloads` are running on the **right** `nodes`. For example, you might want to run a set of `pods` on a high CPU `node`, and run another set of `pods` on a low CPU `node`. You can use `node` selectors to make sure that the **right** `pods` are running on the **right** `nodes`.

<br />

## ***Node Selectors***


Node selectors are **constrained** to `node` `labels`. `Node` `labels` are `key-value` pairs that are attached to `nodes`. `Node` `labels` can be used in `node` `selectors` specified in `pod` definitions. `Node` `selectors` work by ***matching*** `node` `labels` with `pod` `labels`. A `pod` can ***only*** be scheduled onto a `node` if the `node` `labels` ***match*** the `pod` `labels`.

<br />

## ***Node Affinity***

Instead you can use `Node Affinity` to perform the same task. `Node Affinity` is a ***field*** in `pod` definitions. It specifies a set of `rules` that are used to match `nodes` with `pods`. `Node Affinity` can be used in ***conjunction*** with `node` `selectors`. `Node Affinity` can also be used to specify a `preferred` `node` that should be used to run a `pod`. `Node Affinity` is ***more expressive*** than `node` `selectors`. `Node Affinity` can specify ***weight*** for each `rule`. `Node Affinity` can specify ***whether*** or ***not*** a `rule` is ***required***. `Node Affinity` can specify ***how*** `many` `rules` must be ***satisfied*** for the `pod` to be scheduled onto a `node`.


<br />

## ***Basic*** `Commands`

<br />

* to label a `node`

```shell
kubectl label nodes <node-name> <label-key>=<label-value>
```
