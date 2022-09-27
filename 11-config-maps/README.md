# Kubernetes - ***ConfigMaps***

<br>

Just like everything else in kubernetes there are two ways to create a **ConfigMap**. You can either use the `kubectl` command or you can use a **ConfigMap** manifest file.

* example at: `yaml-examples/configmap-description.yaml`


To tie a **ConfigMap** to a **Pod** you can use the `envFrom` or `env` section of the **Pod** manifest file.

* example at: `yaml-examples/configmap-pod.yaml`


<br>

___

<br>

## **Basic Commands**

<br>

* to create a **ConfigMap** using the `kubectl` command, you can use the following command:

```
    kubectl create configmap <configmap name> --from-literal=<key>=<value>
```

* to create a **ConfigMap** using a `manifest file`, you can use the following command:

```
    kubectl create configmap <configmap name> --from-file=<path to file>
``` 

* to get a **ConfigMap** you can use the following command:

```
    kubectl get configmap <configmap name>
```

* to describe a **ConfigMap** you can use the following command:

```
    kubectl describe configmap <configmap name>
```

* to delete a **ConfigMap** you can use the following command:

```
    kubectl delete configmap <configmap name>
```

<br>