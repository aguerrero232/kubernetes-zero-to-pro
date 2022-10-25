# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Volumes*** 💾


## **Description** 👀

`Docker containers` are meant to be **transient** in nature. They are meant to be **created**, **used**, and then **destroyed**. This is a great feature of `containers`, but it also presents a problem when it comes to *state persistence*. Just like in `Docker` the `pods` in `Kubernetes` are also transient. This means that if a pod is destroyed, all of its ***data is lost***. This is a problem if you want to *store data* in a `pod`. To persist data in a `pod` you can use `volumes`. `Volumes` are a way to *store data* in a `pod` that will persist even if the `pod` is destroyed. `Volumes` are also a way to *share data* between `pods`.

<!-- <br />

## **Basic** `Commands` 📝 -->

<br />


## **Examples** 🧩

* `pod` definition with a `volume`

  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
      name: my-pod
  spec: 
      containers:
        - name: alpine
          image: alpine
          command: ["/bin/sh", "-c"]
          args: ["shuf -i 0-100 -n >> /opt/number.out"]
          volumeMounts:
            - mountPath: /opt
              name: data-volume
      volumes:
        - name: data-volume
          hostPath:
            path: /data
            type: Directory
  ```

* `pod` definition with a `volume` to be used in ***pvc** section*

  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: webapp
    namespace: default
  spec:
    containers:
      - name: event-simulator 
        image: kodekloud/event-simulator
        env:            
          - name: LOG_HANDLERS
            value: file
        volumeMounts:
          - mountPath: /log
            name: log-volume        
    volumes:
      - name: log-volume
        hostPath:
          path: /var/log/webapp
          type: Directory
  ```

<br />

[↩️](../README.md)
