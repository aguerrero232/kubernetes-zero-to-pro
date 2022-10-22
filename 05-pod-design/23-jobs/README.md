# **Kubernetes** - ***Jobs***

`Jobs` are a way to run a `pod` to **completion**.  A ``job`` creates one or more `pods` and ensures that a specified number of them successfully terminate.  As `pods` successfully complete, the `job` tracks the successful completions.  When a specified number of successful completions is reached, the `job` itself is complete.  Deleting a `job` will clean up the `pods` it created.

<br>

**Examples** of `jobs`:

* performing a *one-time* task such as *running a script* or *setting up a work directory* for a `deployment`
* *computations for a finite amount of data*, such as **analyzing** a *large data set* or **rendering** a frames of a movie
* and **many other use cases** where you want to run a `pod` to *completion and then stop*.

<br>

## **Creating** *a* `Job`

<br>

By ***default*** Kubernetes will **restart** a `pod` if it fails.  This is **not** a desirable action for a `job`.

* `spec` section of a `pod` that *will not* be **reset** 

    ```yaml
    spec:    
        # default is Always
        # restartPolicy: Always
        # set to Never to run a pod to completion
        restartPolicy: Never
    ```

Sample `job` definition:

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: math-add-job
spec:
    template:
        spec:
            containers:
            - name: math-add
              image: ubuntu
              command: ["expr", "77", "+", "5"]
            restartPolicy: Never
```

## **Basic** `Commands`

<br>

* **get** `jobs`

    ```bash
    kubectl get jobs
    ```
