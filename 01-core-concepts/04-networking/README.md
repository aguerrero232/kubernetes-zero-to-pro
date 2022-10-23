# **Kubernetes** - ***Networking*** 🖧

A `node` has an **IP address** that is used to communicate with other `nodes` in the cluster. If you are using `minikube` you can get the **IP address** of the `node` by running ```minikube ip```. When `kubernetes` is configured **IP addresses** are assigned to `pods`. `Pods` can *communicate with each other* using their **IP addresses**.
  
`Kubernetes` *expects you to follow* fundamental networking principles when you create your applications.  

these principles are:
  * **all** `containers`/`pods` *can communicate to one another* without **NAT**
  * **all** `nodes` *can communicate with all* `containers` without **NAT** and vice versa
  
<br>

## **`Ingress` Networking**

`Ingress` is a collection of rules that allow external traffic to reach services running in a `Kubernetes` cluster. `Ingress` can provide load balancing, SSL termination and name-based virtual hosting. Think of `Ingress` as a layer seven (*application layer*) `load balancer`. It sits in front of your `services` and routes traffic to the `service` that matches the `Ingress` rule. `Ingress` can be configured to give services externally-reachable URLs, load balance traffic, terminate SSL, offer name based virtual hosting, and more.The solution you deploy is called the `Ingress controller`. The set of rules you use to configure `Ingress` are called `Ingress resources`.

A `Kubernetes` cluster **is not** set up with an `Ingress controller` by default.

<br />

## **Examples** 🧩

* ## **`Ingress`** **Controllers** 🎮

  * sample `ingress` ***controller***

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

    * sample `ConfigMap`, needed for the `ingress` ***controllers*** `container` args

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

  `Nginx Ingress Controllers` have *additional intelligence* built into them to monitor the `Kubernetes` cluster for `ingress` **resources**.

  * the `ingress` controller will need the *right set of permissions* to take advantage of the additional intelligence, a `service account` is **required**

    ```yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: nginx-ingress-serviceaccount
    ```

* ## **`Ingress`** ***Resources*** 🧱




[↩️](../)
