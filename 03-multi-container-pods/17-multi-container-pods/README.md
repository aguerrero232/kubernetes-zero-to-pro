# **Kubernetes** - ***Multi Container Pods*** 🐳<sup>🐳</sup>

There are different types of **multi container** `pods`. They include:

* Ambassador
* Adapter
* Sidecar

<br />

## **Examples** 🧩

* sample **multi container** `pod` 🐳<sup>🐳</sup>

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: yellow
    spec:
        containers:
          - name: lemon
            image: busybox
            command: ["sleep", "1000"]
          - name: gold
            image: redis
    ```

<br>

[↩️](../)
