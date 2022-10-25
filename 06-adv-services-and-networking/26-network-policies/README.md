# **Kubernetes** - ***Network Policies*** 🤝

## **Description** 👀

By default `kubernetes` *allows all traffic to and from `pods`*. This is a **security risk** as it *allows `pods` to communicate with each other without any restrictions*. Network policies allow you to restrict traffic to and from `pods`. This is done by creating a network policy object that specifies which `pods` can communicate with each other.

<br>

## **Examples** 🧩

* `network policy` definition

    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
        name: db-policy
        namespace: prod
    spec:
        podSelector:
            matchLabels:
                role: db
        policyTypes:
        # allow egress traffic to pods by not specifying Egress policy type
        #    - Egress
        # allow ingress traffic from pods with role=api
          - Ingress
        ingress:

          - from:

            #           💡💡💡 Very Important Note 💡💡💡
            #
            #   elements can be passed in together as a single rule 
            #   or separately as multiple rules
            #   
            #   example: 
            #     
            #       match pods            
            #           with name=api 
            #           and namespace=prod 
            #               or namespace=non-prod
            #       or match cidr
            #
            #   (pods with name=api && (namespace=prod || namespace=non-prod)) || (cidr with defined <ip-address>/<mask>)
            #
            #   example is implemented below
            #

              - podSelector:
                    matchLabels:
                        name: api
                namespaceSelector:
                     matchLabels:
                        name: non-prod
            # or

            # match with incoming traffic from the cidr defined 
              - ipBlock:
                    cidr: <ip-address>/<mask>

            ports:
              - protocol: TCP
                port: 3306
    ```

* `network policy` with **ingress** and **egress**

    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
        name: db-policy
        namespace: prod
    spec:
        podSelector:
            matchLabels:
                role: db
        policyTypes:
            - Egress
            - Ingress
        ingress:
          - from:
              - podSelector:
                    matchLabels:
                        name: api
            ports:
              - protocol: TCP
                port: 3306
        egress:
          - to:
              - ipBlock:
                    cidr: <ip-address>/<mask>

            ports:
              - protocol: TCP
                port: 80
    ```

<br>

[↩️](../README.md)
