# <img src="../../assets/img/k8s.png" width="30px"> **Kubernetes** - ***Deployments*** 🚀

## **Description** 👀

`Deployments` are the preferred way to manage pods. They are a **higher level abstraction** than`Replica Sets`. They allow you to *define the desired state* of your application, and the `controller` will make sure that the current state matches the desired state.

<br>

## ***Updates*** *and* ***Rollbacks*** 🔄

* `Deployments` allow you to **`update` your application without downtime**.

* There are **two methods** to `update` your application:

  * **`Rolling Update`** - The new version of the application is *deployed* in stages. The old version is still running while the new version is being *deployed*. Once the new version is *deployed*, the old version is *terminated*.

  * **`Recreate`** - The old version of the application is terminated *before* the new version is *deployed*.

* `rollbacks` are also possible. You can `rollback` to a *previous version* of your application.

<br>

## **Basic** `Commands` 📝

* **update** a `deployment` &nbsp; (`rolling update`)

  ```bash
  kubectl apply -f <yaml-file>
  ```

  ```bash
  kubectl set image deployment/<deployment-name> <new-image>
  ```

* **get** list of `deployments`

  ```bash
  kubectl get deployments
  ```

* **get** *descriptive information* on the desired `deployment`

  ```bash
  kubectl describe deployment <deployment-name>
  ```

* **get** the *rollout status* of the `deployment`

  ```bash
  kubectl rollout status deployment/<deployment-name>
  ```

* **get** the *rollout history* of the `deployment`

  ```bash
  kubectl rollout history deployment/<deployment-name>
  ```

* **rollback** to a *previous version* of the `deployment`

  ```bash
  kubectl rollout undo deployment/<deployment-name>
  ```

* ***use*** the `--to-revision` flag to *specify* the `revision number` to **rollback** to.

  ```bash
  kubectl rollout undo deployment/<deployment-name> --to-revision=<revision-number>
  ```

* **view** `deployment` at a specific `revision`

  ```bash
  kubectl rollout history deployment <deployment-name> --revision=<revision-number>
  ```

* **use** the `--record` flag to *save the command used* to **create/update** a `deployment`

  ```bash
  kubectl apply -f <yaml-file> --record=true
  ```

<br />

## **Examples** 🧩

* sample `deployment` definition

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: myapp-depl
    labels:
      tier: front-end
  spec: 
    template:
      metadata:
        name: nginx-pod
        labels:
          app: myapp
          type: front-end
      spec:
        containers:
          - name: nginx
            image: nginx
    replicas: 6
    selector: 
      matchLabels:
        app: myapp
  ```

* sample `deployment` definition with `web-hook`
  * sample `service` definition is in the ***core-concepts/services*** section
  * sample `tls secret` is in the ***configuration/secrets*** section

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: webhook-server
    namespace: webhook-demo
    labels:
      app: webhook-server
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: webhook-server
    template:
      metadata:
        labels:
          app: webhook-server
      spec:
        securityContext:
          runAsNonRoot: true
          runAsUser: 1234
        containers:
        - name: server
          image: stackrox/admission-controller-webhook-demo:latest
          imagePullPolicy: Always
          ports:
          - containerPort: 8443
            name: webhook-api
          volumeMounts:
          - name: webhook-tls-certs
            mountPath: /run/secrets/tls
            readOnly: true
        volumes:
        - name: webhook-tls-certs
          secret:
            secretName: webhook-server-tls
  ```

* sample `web-hook` definition for deployment

  ```yaml
  apiVersion: admissionregistration.k8s.io/v1
  kind: MutatingWebhookConfiguration
  metadata:
    name: demo-webhook
  webhooks:
    - name: webhook-server.webhook-demo.svc
      clientConfig:
        service:
          name: webhook-server
          namespace: webhook-demo
          path: "/mutate"
        caBundle: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURQekNDQWllZ0F3SUJBZ0lVSzl5dHRGRTdMR3QxU3V4UWROZThjbStYWlZNd0RRWUpLb1pJaHZjTkFRRUwKQlFBd0x6RXRNQ3NHQTFVRUF3d2tRV1J0YVhOemFXOXVJRU52Ym5SeWIyeHNaWElnVjJWaWFHOXZheUJFWlcxdgpJRU5CTUI0WERUSXlNVEF6TVRFNU5EUXhNbG9YRFRJeU1URXpNREU1TkRReE1sb3dMekV0TUNzR0ExVUVBd3drClFXUnRhWE56YVc5dUlFTnZiblJ5YjJ4c1pYSWdWMlZpYUc5dmF5QkVaVzF2SUVOQk1JSUJJakFOQmdrcWhraUcKOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQTBGZ0UvQUVNVGJIL1FyN09USWFRVkcxdnM0NkNiRUl2UHFEcQpSTjY1SHA2eTJTeDh1TjFzdDRRNTZiaWpYTVYydmhjdzR1N3pidFBpUmlMZVlMTEFLMkx4NTl0eUZIcXBDcEZhCjcrNjkzVks2MGtlVlkrSEN4RlhRcGZNMzlhK0FQNW9uZFJVSkc5emJrY3FyQ0JCM1dQaTlnZmhGR0xxc1hydEgKakYzRjI2Z29xUG9GeCtaT2Y3MjQrdGtkT3hvOGp6UmZuUzhnVE5vTnRvSFhEeEt5Vk9vT051R2VNbHRIemZMMQo3cG9kZ25IQzJXRjJ6Tk9wMkh2cnR2Q1VLbXFVdjRBNzlzZWtHelhkRUxpNm9rZ2VyTGNad1NGOXUxcGFFVkhGCkc0cjVaMEdVSTNLN0hzaDE2ekYrUmFFbmZGbTMydzdSZytCOEtGejVMMDQxQi9vandRSURBUUFCbzFNd1VUQWQKQmdOVkhRNEVGZ1FVaFByYlZKTGlCcy94MHgwNXlFRTZOOGNZUkFvd0h3WURWUjBqQkJnd0ZvQVVoUHJiVkpMaQpCcy94MHgwNXlFRTZOOGNZUkFvd0R3WURWUjBUQVFIL0JBVXdBd0VCL3pBTkJna3Foa2lHOXcwQkFRc0ZBQU9DCkFRRUFMZUszUldPU1Bqa0R1aWJaQnc3YjRFVFZnQnE3ZCt6UGFzYng0NEorQUczS1JlWDRWamcza0Rtb2lhZEwKb1htc0RVSFV1N1E4R3ZKaGl0NDlMb2ZycnM3UnZMcUFPb0RRYkxkQ3c1RWpnRytBWkZ1N0JOR284U0RkZ2NnegpWbEtJcGlCdmpFTVp0MXRENDNEMEJIa2JERGZ6bTNSdUlLRW05WFhTeWJqTUp1U0lxais5WXF3OHdkZWJqa2E0CkJwNldvc3U1WGJaT3d1VFhEaWhzMk1nWkt2NDZwNkJDdWN2MWs4cmFUR2JHMG1wL3hzN0hDdkhXZUZjK1pnYnQKeGNiaDFxZ3BkN2E3OFpqVXN2NG56RzhnOE1JOU80ZUNpMDN3RnRCV1J1SHh0QzBxbUZtcSt3d3QzUzMyMDFzWgpySnR1c1R4TEFlQXRWVjlXQkhLeWRyY2dRQT09Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
      rules:
        - operations: [ "CREATE" ]
          apiGroups: [""]
          apiVersions: ["v1"]
          resources: ["pods"]
      admissionReviewVersions: ["v1beta1"]
      sideEffects: None
  ```

<br>

[↩️](../README.md)
