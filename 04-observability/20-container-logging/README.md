# **Kubernetes** - ***Container Logging***

`Logging` is a **critical** part of **monitoring** and **debugging** `containerized` applications. `Kubernetes` provides a **native** solution to **collect** and **store** `container` logs.

<br>

## **Basic** `Commands`

* **view** `logs` for a `pod`
  * `-f`: follow the `logs` as they are written, *simmilar to docker*

    ```bash
    kubectl logs -f <pod-name>
    ```

* if there are multiple `containers` in the `pod`, you must specify the `container` name

  ```bash
  kubectl logs -f <pod-name> -c <container-name>
  ```

<br>

[↩️ **back**](../)
