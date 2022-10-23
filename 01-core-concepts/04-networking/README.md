# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Networking*** 🖧

A `node` has an **IP address** that is used to communicate with other `nodes` in the cluster. If you are using `minikube` you can get the **IP address** of the `node` by running ```minikube ip```. When `kubernetes` is configured **IP addresses** are assigned to `pods`. `Pods` can *communicate with each other* using their **IP addresses**.
  
`Kubernetes` *expects you to follow* fundamental networking principles when you create your applications.  

these principles are:

* **all** `containers`/`pods` *can communicate to one another* without **NAT**
* **all** `nodes` *can communicate with all* `containers` without **NAT** and vice versa
  
<br>

## **`Ingress` Networking** ⚖️

* 🗎 [**k8 ingress documentation**](https://kubernetes.io/docs/concepts/services-networking/ingress/)

`Ingress` is a collection of rules that allow external traffic to reach services running in a `Kubernetes` cluster. `Ingress` can provide load balancing, SSL termination and name-based virtual hosting. Think of `Ingress` as a layer seven (*application layer*) `load balancer`. It sits in front of your `services` and routes traffic to the `service` that matches the `Ingress` rule. `Ingress` can be configured to give services externally-reachable URLs, load balance traffic, terminate SSL, offer name based virtual hosting, and more.The solution you deploy is called the `Ingress controller`. The set of rules you use to configure `Ingress` are called `Ingress resources`.

A `Kubernetes` cluster **is not** set up with an `Ingress controller` by default.

<br />

## **Basic** `Commands` 📝

* **view** details of `ingress` objects

  ```bash
  kubectl describe ingress <ingress-object-name>
  ```

* imperatively **create** an `ingress` object

  ```bash
  kubectl create ingress <ingress-object-name> --rule=<host/path=service:port> --backend=<backend>
  ```

<br>

## **Examples** 🧩

* ## **`Ingress`** **Controllers** 🎮

  * sample `ingress` ***controller*** definition

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-ingress-controller
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: nginx-ingress
      template:
        metadata:
          labels:
            app: nginx-ingress
        spec:
          containers:
          - name: nginx-ingress-controller
            image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0
            args:
              - /nginx-ingress-controller
              - --default-backend-service=$(POD_NAMESPACE)/default-http-backend
              # create a config map object as a pass through to the nginx-controller for custom configuration
              - --configmap=$(POD_NAMESPACE)/nginx-configuration
            # you MUST pass the POD_NAME and POD_NAMESPACE as an env variables to the nginx-ingress-controller
            env:
              - name: POD_NAME
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.name
              - name: POD_NAMESPACE
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.namespace
            # specify the ports used by the nginx-ingress-controller
            ports:
              - name: http
                containerPort: 80
              - name: https
                containerPort: 443
    ```

    * sample `ConfigMap`, needed for the `ingress` controller `container` args

      ```yaml
      apiVersion: v1
      kind: ConfigMap
      metadata:
        name: nginx-configuration
      data:
        # put your custom nginx configuration here
      ```

  * then create a service to expose the `ingress` controller to the external world

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-ingress
    spec:
      type: NodePort
      ports:
      - port: 80
        targetPort: 80
        protocol: TCP
        name: http
      - port: 443
        targetPort: 443
        protocol: TCP
        name: https
      selector:
        app: nginx-ingress
    ```

    * the `ingress` controller will need the *right set of permissions* to take advantage of the additional intelligence, a `service account` is **required**

      ```yaml
      apiVersion: v1
      kind: ServiceAccount
      metadata:
        name: nginx-ingress-serviceaccount
      ```

  `Nginx Ingress Controllers` have *additional intelligence* built into them to monitor the `Kubernetes` cluster for `ingress` **resources**.
  * 🗎 [**nginx ingress controller documentation**](https://kubernetes.github.io/ingress-nginx/examples/)

<br>

* ## **`Ingress`** ***Resources*** 🧱

  An `Ingress` resource is a *set of rules* used to configure the `Ingress controller` to route traffic to the `services` that match the `Ingress rules`. `Ingress` resources are *namespaced* and can be created in any `namespace` that you want to expose your `services` from.

  * sample `ingress` **resource**  definition

    ```yaml
      apiVersion: networking.k8s.io/v1
      kind: Ingress
      metadata:
        name: ingress-wear-watch
        namespace: app-space
      spec:
        rules:
          - http:
              paths:
              - backend:
                  service:
                    name: wear-service
                    port:
                      number: 8080
                path: /wear
                pathType: Prefix
              - backend:
                  service:
                    name: video-service
                    port:
                      number: 8080
                path: /watch
                pathType: Prefix
      ```

    * to route **domain names** users must define a `host` in the `ingress` resource `spec.rules` section

  * **create** `ingress` resource imperatively

    ``` bash
    kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"
    ```

  * video service

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: video-service
      namespace: app-space
    spec:
      clusterIP: 10.96.151.193
      clusterIPs:
      - 10.96.151.193
      ports:
      - port: 8080
        protocol: TCP
        targetPort: 8080
      selector:
        app: webapp-video
      sessionAffinity: None
      type: ClusterIP
    ```

  * wear service

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: wear-service
      namespace: app-space
    spec:
      clusterIP: 10.102.76.86
      clusterIPs:
      - 10.102.76.86
      ports:
      - port: 8080
        protocol: TCP
        targetPort: 8080
      selector:
        app: webapp-wear
      sessionAffinity: None
      type: ClusterIP
    ```

  * default `backend` service

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: default-backend-service
      namespace: app-space
    spec:
      type: ClusterIP
      clusterIP: 10.104.209.223
      clusterIPs:
        - 10.104.209.223
      ports:
      - port: 80
        protocol: TCP
        targetPort: 8080
      selector:
        app: default-backend
    ```

  * more ➜ `service` and `ingress` resources

    * **`service`**

      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: pay-service
        namespace: critical-space
      spec:
        clusterIP: 10.102.93.253
        clusterIPs:
        - 10.102.93.253
        ipFamilies:
        - IPv4
        ports:
        - port: 8282
          protocol: TCP
          targetPort: 8080
        selector:
          app: webapp-pay
        type: ClusterIP
      ```

    * **`ingress`**

      ```yaml
      apiVersion: networking.k8s.io/v1
      kind: Ingress
      metadata:
        name: ingress-pay
        namespace: critical-space 
        annotations:
          nginx.ingress.kubernetes.io/rewrite-target: /
      spec:
        rules:
        - http:
            paths:
            - backend:
                service:
                  name: pay-service
                  port:
                    number: 8282
              path: /pay
              pathType: Prefix
      ```

      * ***ReWrite*** the `URL` when a *request is passed* to applications. Instead of using the same path that user typed in specify the `rewrite-target` option. This **rewrites** the `URL` by replacing whatever is under **rules ➜ http ➜ paths ➜ path**.

        ```yaml
          annotations:
            nginx.ingress.kubernetes.io/rewrite-target: /
        ```

        * 🗎 [**example from the k8 nginx ingress documentation**](https://kubernetes.github.io/ingress-nginx/examples/rewrite/)

<br>

## ***Basic Steps*** 👣

1. create a namespace for ingress related objects

    ```bash
    kubectl create namespace ingress-space
    ```

    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
      creationTimestamp: "2022-10-23T19:48:00Z"
      managedFields:
      - apiVersion: v1
        fieldsType: FieldsV1
        fieldsV1:
          f:status:
            f:phase: {}
        manager: kubectl-create
        operation: Update
        time: "2022-10-23T19:48:00Z"
      name: ingress-space
      resourceVersion: "7557"
      uid: 4c9214e5-1d83-427e-b93b-12fec40ac3d0
    spec:
      finalizers:
      - kubernetes
    status:
      phase: Active
    ```

2. create a configmap for the ingress controller in the ingress-space namespace

    ```bash
    kubectl create configmap nginx-configuration -n ingress-space
    ```

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      creationTimestamp: "2022-10-23T19:48:42Z"
      name: nginx-configuration
      namespace: ingress-space
      resourceVersion: "7614"
      uid: 9fbd2239-1265-4615-834c-752349e668da
    ```

3. create a service account for the ingress controller in the ingress-space namespace

    ```bash
    kubectl create serviceaccount ingress-serviceaccount -n ingress-space
    ```

    ```yaml
      apiVersion: v1
      kind: ServiceAccount
      metadata:
        creationTimestamp: "2022-10-23T19:49:18Z"
        name: ingress-serviceaccount
        namespace: ingress-space
        resourceVersion: "7659"
        uid: ca003d54-4978-4e40-aaad-99c522c14f5d
      secrets:
      - name: ingress-serviceaccount-token-nrm2r
    ```

4. create roles and role-bindings for the service account ingress-serviceaccount

    * `ingress-role`

        ```yaml
        apiVersion: rbac.authorization.k8s.io/v1
        kind: Role
        metadata:
          creationTimestamp: "2022-10-23T19:49:25Z"
          labels:
            app.kubernetes.io/name: ingress-nginx
            app.kubernetes.io/part-of: ingress-nginx
          managedFields:
          - apiVersion: rbac.authorization.k8s.io/v1
            fieldsType: FieldsV1
            fieldsV1:
              f:metadata:
                f:labels:
                  .: {}
                  f:app.kubernetes.io/name: {}
                  f:app.kubernetes.io/part-of: {}
              f:rules: {}
            manager: python-requests
            operation: Update
            time: "2022-10-23T19:49:25Z"
          name: ingress-role
          namespace: ingress-space
          resourceVersion: "7669"
          uid: 4e8667a7-7b9c-4fd7-a796-cd85e2cc2251
        rules:
        - apiGroups:
          - ""
          resources:
          - configmaps
          - pods
          - secrets
          - namespaces
          verbs:
          - get
        - apiGroups:
          - ""
          resourceNames:
          - ingress-controller-leader-nginx
          resources:
          - configmaps
          verbs:
          - get
          - update
        - apiGroups:
          - ""
          resources:
          - configmaps
          verbs:
          - create
        - apiGroups:
          - ""
          resources:
          - endpoints
          verbs:
          - get
        ```

    * `ingress-role-binding`

        ```yaml
        apiVersion: rbac.authorization.k8s.io/v1
        kind: RoleBinding
        metadata:
          creationTimestamp: "2022-10-23T19:49:25Z"
          labels:
            app.kubernetes.io/name: ingress-nginx
            app.kubernetes.io/part-of: ingress-nginx
          managedFields:
          - apiVersion: rbac.authorization.k8s.io/v1
            fieldsType: FieldsV1
            fieldsV1:
              f:metadata:
                f:labels:
                  .: {}
                  f:app.kubernetes.io/name: {}
                  f:app.kubernetes.io/part-of: {}
              f:roleRef:
                f:apiGroup: {}
                f:kind: {}
                f:name: {}
              f:subjects: {}
            manager: python-requests
            operation: Update
            time: "2022-10-23T19:49:25Z"
          name: ingress-role-binding
          namespace: ingress-space
          resourceVersion: "7670"
          uid: 05147ae6-18ec-4502-a2a9-fb55f664ceb7
        roleRef:
          apiGroup: rbac.authorization.k8s.io
          kind: Role
          name: ingress-role
        subjects:
        - kind: ServiceAccount
          name: ingress-serviceaccount
        ```

5. create ingress controller deployment

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: ingress-controller
      namespace: ingress-space
    spec:
      replicas: 1
      selector:
        matchLabels:
          name: nginx-ingress
      template:
        metadata:
          labels:
            name: nginx-ingress
        spec:
          serviceAccountName: ingress-serviceaccount
          containers:
            - name: nginx-ingress-controller
              image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0
              args:
                - /nginx-ingress-controller
                - --configmap=$(POD_NAMESPACE)/nginx-configuration
                - --default-backend-service=app-space/default-http-backend
              env:
                - name: POD_NAME
                  valueFrom:
                    fieldRef:
                      fieldPath: metadata.name
                - name: POD_NAMESPACE
                  valueFrom:
                    fieldRef:
                      fieldPath: metadata.namespace
              ports:
                - name: http
                  containerPort: 80
                - name: https
                  containerPort: 443
    ```

6. create ingress service to expose nginx ingress controller

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: ingress
      namespace: ingress-space
    spec:
      type: NodePort
      ports:
        - port: 80
          targetPort: 80
          protocol: TCP
          nodePort: 30080
          name: http
        - port: 443
          targetPort: 443
          protocol: TCP
          name: https 
      selector:
        name: nginx-ingress
    ```

7. create ingress resource

    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: ingress-wear-watch
      namespace: app-space 
      annotations:
        nginx.ingress.kubernetes.io/rewrite-target: /
        nginx.ingress.kubernetes.io/ssl-redirect: "false"
    spec:
      rules:
      - http:
          paths:
          - backend:
              service:
                name: wear-service
                port:
                  number: 8080
            path: /wear
            pathType: Prefix
          - backend:
              service:
                name: video-service
                port:
                  number: 8080
            path: /watch
            pathType: Prefix
    ```
     * service definitions are found in the above examples
     * deployment definitions can be found in the [**yaml-examples**](yaml-examples/) folder
       * yaml-example/***deafult-backend.yaml***
       * yaml-example/***webapp-video.yaml***
       * yaml-example/***webapp-wear.yaml***


<br>

[↩️](../README.md)
