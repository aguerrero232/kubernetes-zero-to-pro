# **Kubernetes** - ***Labels***, ***Selectors***, *and* ***Annotations***

**Filter** and *group* `pods` using `labels` and `selectors`. `Annotations` are used to add *metadata* to `pods`.

<br />

## **Basic** `Commands`

<br />

* **select** `pods` with label

    ```shell
    kubectl get pods --selector <label-name>=<label-value>
    ```

* **count** `pods` with label

    ```shell
    kubectl get pods --selector <label-name>=<label-value> --no-headers | wc -l
    ```

* **select** all with multiple labels

    ```shell
    kubectl get all --selector <label-name>=<label-value>,<label-name>=<label-value>
    ```
