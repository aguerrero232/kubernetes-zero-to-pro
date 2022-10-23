# **Kubernetes** - ***Init Containers*** 💥

At times you may want to **run** a `process` that **runs** to completion in a `container`. For example a `process` that pulls a code or binary from a repository that will be used by the main web application. That is a task that will be **run** only one time when the `pod` is first **created**. Or a `process` that waits for an external service or `database` to be up before the actual application starts. That's where `initContainers` come in.

In other words `initContainers` are `containers` that ***run to completion before*** the `main` `container` starts. They are **useful** for tasks such as initializing a `database`, pulling a `code` from a `repository`, or other **utilities**.

<br>

## **Examples** 🧩

* sample **init container** definition

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: myapp-pod
        labels:
            app: myapp
    spec:
        containers:
          - name: myapp-container
            image: busybox:1.28
            command: ["sh", "-c", "echo The app is running! && sleep 3600"]
        initContainers:
          - name: init-myservice
            image: busybox
            command:
                [
                "sh",
                "-c",
                "git clone <some-repository-that-will-be-used-by-application> ;",
                ]
    ```

* different way to declare commands in container

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: red
    spec:
        containers:
          - image: busybox:1.28
            name: red-container-bb
            command:
              - sh
              - -c
              - echo The app is running! && sleep 3600
        initContainers:
          - name: red-init-bb
            image: busybox
            command:
                - "sleep"
                - "20"
            restartPolicy: Always
    ```

<br />

[↩️](../)
