# **Kubernetes** - ***Readiness*** *And* ***Liveness Probes***

At times you may want to **check** if a `container` is **ready** to **serve** requests. Or you may want to **check** if a `container` is **alive** and **healthy**. That's where `readinessProbes` and `livenessProbes` come in.


## **Readiness Probes**

`readinessProbes` are used to **check** if a `container` is **ready** to **serve** requests. If a `readinessProbe` fails, the `container` will **not** receive any traffic from a `service`. However, if a `readinessProbe` fails, the `container` will **not** be restarted, unless it is also `unhealthy`.

## **Liveness Probes**

`livenessProbes` are used to **check** if a `container` is **alive** and **healthy**. If a `livenessProbe` fails, the `container` will be restarted. `livenessProbes` are useful when `containers` become **unresponsive** due to **memory leaks** or **deadlocks**.



<br>

↩️ [**back**](../)
