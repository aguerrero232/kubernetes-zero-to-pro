# <img src="../../assets/img/k8s.png" width="30px"> **Kubernetes** - ***Networking*** 🖧


## **Description** 👀

A `node` has an **IP address** that is used to communicate with other `nodes` in the cluster. If you are using `minikube` you can get the **IP address** of the `node` by running ```minikube ip```. When `Kubernetes` is configured **IP addresses** are assigned to `pods`. `Pods` can *communicate with each other* using their **IP addresses**.
  
`Kubernetes` *expects you to follow* fundamental networking principles when you create your applications.  

these principles are:

* **all** `containers`/`pods` *can communicate to one another* without **NAT**
* **all** `nodes` *can communicate with all* `containers` without **NAT** and vice versa
  
<br>


[↩️](../README.md)
