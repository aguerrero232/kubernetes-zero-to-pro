# <img src="../assets/img/k8s.png" width="30px"> **Kubernetes** - ***Section 5:*** `Pod Design` 💠

## ***Table*** *of* ***`Contents`*** 📜

* 🏠 [**home**](../README.md)
* 💠 **pod-design**
  * 🏷️ [**labels selectors** *and* **annotations**](22-labels-selectors-annotations/README.md)
    * 🔗 <a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/" target="_blank">k8s labels selectors and annotations documentation</a>
  * 👔 [**jobs**](23-jobs/README.md)
    * 🔗 <a href="https://kubernetes.io/docs/concepts/workloads/controllers/job/" target="_blank">k8s jobs documentation</a>
  * ⏳ [**cron jobs**](24-cron-jobs/README.md)
    * 🔗 <a href="https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/" target="_blank">k8s cron jobs documentation</a>

<br />

## **Description** 👀

In general, **design patterns** are implemented to *solve and reuse common well thought out architectures*. **Design patterns** also introduce **efficiency** into applications, reducing overhead and provides a way to reuse `containers` across applications. There are several ways to group or to enhance containers inside of ***Kubernetes*** `Pods`. These patterns can be categorized as single `node`, `multi-container` patterns or you can use the more advanced `multi-node` applications patterns.
