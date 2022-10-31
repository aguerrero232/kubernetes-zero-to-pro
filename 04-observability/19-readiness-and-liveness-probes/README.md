# <img src="../../assets/img/k8s.png" width="30px"> **Kubernetes** - ***Readiness*** *And* ***Liveness Probes*** 🛸

## **Description** 👀

At times you may want to **check** if a `container` is **ready** to **serve** requests. Or you may want to **check** if a `container` is **alive** and **healthy**. That's where `readinessProbes` and `livenessProbes` come in.
* ### **Readiness Probes**

    `readinessProbes` are used to **check** if a `container` is **ready** to **serve** requests. If a `readinessProbe` fails, the `container` will **not** receive any traffic from a `service`. However, if a `readinessProbe` fails, the `container` will **not** be restarted, unless it is also `unhealthy`.
* ### **Liveness Probes** 

    `livenessProbes` are used to **check** if a `container` is **alive** and **healthy**. If a `livenessProbe` fails, the `container` will be restarted. `livenessProbes` are useful when `containers` become **unresponsive** due to **memory leaks** or **deadlocks**.

<br>

## **Examples** 🧩

* sample `readinessProbe` definition

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: readiness-probe
    spec:
        containers:
          - name: readiness-probe
            image: nginx
            readinessProbe:
                httpGet:
                path: /index.html
                port: 80

                # for tcp
                # tcpSocket:
                #   port: 80

                # for exec
                # exec:
                #   command:
                #     - cat
                #     - /tmp/healthy

                initialDelaySeconds: 5
                periodSeconds: 5
    ```

* sample `livenessProbe` definition

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: readiness-probe
    spec:
        containers:
          - name: web-app
            image: web-app
            ports:
              - containerPort: 8080
            livenessProbe:
                httpGet:
                path: /health
                port: 8080

                # for tcp
                # tcpSocket:
                #   port: 8080
            
                # for exec
                # exec:
                #   command:
                #     - cat
                #     - /tmp/healthy
                
                initialDelaySeconds: 5
                periodSeconds: 5
    ```

* sample `pod` with `readiness` and `liveness` **probe**

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        labels:
            name: simple-webapp
        name: simple-webapp
    spec:
        containers:
        - name: simple-webapp
            image: kodekloud/webapp-delayed-start
            imagePullPolicy: Always
            env:
            - name: APP_START_DELAY
                value: "80"
            ports:
            - containerPort: 8080
            protocol: TCP
            readinessProbe:
                httpGet:
                    path: /ready
                    port: 8080
            livenessProbe:
                httpGet:
                    path: /live
                    port: 8080
                initialDelaySeconds: 80
                periodSeconds: 1
    ```

<br>

[↩️](../README.md)
