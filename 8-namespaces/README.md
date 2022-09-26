# Kubernetes - ***Namespaces***

Namespaces provides a mechanism for isolating groups of resources within a single cluster. 
* Names of resources need to be unique within a namespace, but not across namespaces.
* Intended for use in environments with many users spread across multiple teams, or projects.
* Can be used to set a resouce quota
___

<br>

## ***Basic Commands***

<br>

* list current namespaces
  
  ```
  kubectl get namespace
  ```

  * create a namespace
  
  ```
  kubectl create namespace <namespace-name>
  ```

  * delete a namespace
  
  ```
  kubectl delete namespace <namespace-name>
  ```

  * get all resources in a namespace
  
  ```
  kubectl get all --namespace <namespace-name>
  ```