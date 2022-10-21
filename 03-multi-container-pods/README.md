# **Kubernetes** - ***Section 3:*** `Multi Container Pods`

At times you may need two `services` to *work together*. For example, you may need a web server and a logging service to *work together*. In this case, you can use a `multi container pod`. To add another `container` to your `pod` all you have to do is define it in the `pods` yaml spec section under `containers`.
