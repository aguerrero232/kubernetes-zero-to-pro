# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Labels***, ***Selectors***, *and* ***Annotations*** 🏷️

**Filter** and *group* `pods` using `labels` and `selectors`. `Annotations` are used to add *metadata* to `pods`.

<br />

## **Basic** `Commands` 📝

* **select** `pods` with label

    ```bash
    kubectl get pods --selector <label-name>=<label-value>
    ```

* **count** `pods` with label

    ```bash
    kubectl get pods --selector <label-name>=<label-value> --no-headers | wc -l
    ```

* **select** all with multiple labels

    ```bash
    kubectl get all --selector <label-name>=<label-value>,<label-name>=<label-value>
    ```

<br>

## **Examples** 🧩

* sample `pod` with `label`

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: app-1
        labels:
            app: app-1
            function: front-end
    spec:
        containers:
          - name: nginx-app-1
            image: nginx:1.7.9
            ports:
              - containerPort: 8080
    ```

<br />

[↩️](../)
