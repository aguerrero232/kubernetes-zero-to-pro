# <img src="../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***Section 3:*** `Multi Container Pods` 🐳<sup>🐳</sup>

## ***Table*** *of* ***`Contents`*** 📜

* 🏠 [**home**](https://github.com/aguerrero232/kubernetes-zero-to-pro/blob/main/README.md)
* 🐳<sup>🐳</sup> **multi-container-pods**
  * 🐳<sup>🐳</sup> [**multi-container-pods**](17-multi-container-pods/README.md)
  * 💥 [**init containers**](18-init-containers/README.md)

<br />

At times you may need two `services` to *work together*. For example, you may need a web server and a logging service to *work together*. In this case, you can use a `multi container pod`. To add another `container` to your `pod` all you have to do is define it in the `pods` yaml spec section under `containers`.
