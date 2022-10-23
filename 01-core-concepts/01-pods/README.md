# **Kubernetes** - ***Pods*** 🐋🐳🐋🐳

A `pod` is a **single instance** of an application and is the **simplest object** you can create in `kubernetes`, usually have a 1:1 relationship with `containers`. `Pods` can have multiple `containers`, but they are usually `containers` of different types that are ***tightly*** coupled.

<br>

## ***Basic*** `Commands` 📝

- **get** *minimal* info about `pods` on cluster

  ```bash
  kubectl get pods
  ```

- **get** *more* info about a `pod`

  ```bash
  kubectl get pods -o wide
  ```

- **get** *even more* information about a `pod`

  ```bash
  kubectl describe pod <pod-name>
  ```

- **get** `pod` in `yaml` format

  ```bash
  kubectl get pod <pod-name> -o yaml
  ```

- **enter** a `pod`

    ```bash
    kubectl exec -it <pod-name> -- /bin/bash
    ```

- **create** a `pod`
  
  ```bash
  kubectl run <pod-name> --image=<image-name>
  ```

- **edit** a `pod`

  ```bash
  kubectl edit pod <pod-name>
  ```

- If you are *not* given a `pod` definition file, you may **extract** the definition to a file using the below command, then **edit** the file to make the *necessary changes*, **delete** and **re-create** the `pod`.

  ```bash
  kubectl get pod <pod-name> -o yaml > pod-definition.yaml
  ```

- **delete** a `pod`

  ```bash
  kubectl delete pod <pod-name>
  ```

- **view** the *containers user* in a `pod`

    ```bash
    kubectl exec <pod-name> -- whoami
    ```

<br>

## **Examples** 📚


* simple `pod` definition

  ```yaml
  apiVersion: v1
  # kind refers to the type of object that will be created
  kind: Pod
  # data about the data that will be created
  metadata:
    name: myapp-pod
    labels:
      app: myapp
      type: testing
  # specification section, providing additional information to kubernetes about the object
  spec:
    containers:
      - name: nginx-container
        image: nginx
  ```




- **define** ***environment variables*** *for a* `container`

  ```yaml
    spec:
      containers:
      - name: <container name>
        image: <image name>
        env:
        - name: DEMO_GREETING
          value: "Hello from the environment"
        - name: DEMO_FAREWELL
          value: "Such a sweet sorrow"
  ```

- **define** ***security context*** *for a* `container`

  ```yaml
    spec:
      containers:
      - name: <container name>
        image: <image name>
        securityContext:
          runAsUser: 1000
          capabilities:
            add: ["MAC_ADMIN"]
  ```

  - `capabilties` are a *set of linux kernel capabilities* that can be **added** to or **removed** from a `container`
  - `capabilities` are only available at the `container` level, **not at** the `pod` level

<br>

[↩️ **back**](../)
