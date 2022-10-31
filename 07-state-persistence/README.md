# <img src="../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Section 7:*** **State Persistence** 🗄️

## ***Table*** *of* ***`Contents`*** 📜

* 🏠 [**home**](../README.md)
* 🗄️ **state persistence**
  * 💾 [**volumes**](27-volumes/README.md)
  * 🏰 [**persistent volumes**](28-persistent-volumes/README.md)
  * 🚩 [**persistent volume claims**](29-persistent-volume-claims/README.md)
  * 📦 [**storage classes**](30-storage-classes/README.md)
  * 🌟 [**stateful sets**](31-stateful-sets/README.md)
  * 🧟 [**headless service**](32-headless-service/README.md)
* 🔗 **links**
  * 🚩 [***k8s claims as volumes documentation***](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#claims-as-volumes)

<br />

## **Description** 👀

`Pods` in Kubernetes are **ephemeral** in nature. They can easily be created and destroyed. This is a problem for stateful applications. Stateful applications require some form of stable storage. Kubernetes provides multiple ways to persist data, that will be covered in this section.
