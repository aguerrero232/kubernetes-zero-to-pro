# **Kubernetes** - ***Jobs*** 👔

`Jobs` are a way to run a `pod` to **completion**.  A ``job`` creates one or more `pods` and ensures that a specified number of them successfully terminate.  As `pods` successfully complete, the `job` tracks the successful completions.  When a specified number of successful completions is reached, the `job` itself is complete.  Deleting a `job` will clean up the `pods` it created.

<br>

## **Examples** of `jobs` 🧑‍💼

* performing a *one-time* task such as *running a script* or *setting up a work directory* for a `deployment`
* *computations for a finite amount of data*, such as **analyzing** a *large data set* or **rendering** a frames of a movie
* and **many other use cases** where you want to run a `pod` to *completion and then stop*.

<br>

## **Basic** `Commands` 📝

* **get** `jobs`

    ```bash
    kubectl get jobs
    ```

* **output** `job` logs

    ```bash
    kubectl logs <job-pod-name>
    ```

<br />

## **Creating** *a* `Job` 🛠️

By ***default*** Kubernetes will **restart** a `pod` if it fails.  This is **not** a desirable action for a `job`.

* `spec` section of a `pod` that *will not* be **reset**

    ```yaml
    spec:    
        # default is Always
        # restartPolicy: Always
        # set to Never to run a pod to completion
        restartPolicy: Never
    ```

* sample `job` definition:

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
        name: math-add-job
    spec:
        # to run multiple of the same job at the same time set completions to a number greater than 1
        # by default the pods are made one after the other
        completions: 3
        template:
            spec:
                containers:
                  - name: math-add
                    image: ubuntu
                    command: ["expr", "77", "+", "5"]
                    restartPolicy: Never
    ```

* to run `jobs` in `parallel` set `spec.parallelism` to a number greater than 1

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
        name: math-add-job
    spec:
        completions: 3
        # to run jobs in parallel set parallelism to a number greater than 1
        parallelism: 3
        template:
            spec:
                containers:
                  - name: math-add
                    image: ubuntu
                    command: ["expr", "77", "+", "5"]
                    restartPolicy: Never
    ```  

<br>

## **Examples** 🧩

* sample `job` definition

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
        name: throw-dice-job
    spec:
        completions: 1
        template:
            metadata:
                name: throw-dice-pod
            spec:
                containers:
                - image: kodekloud/throw-dice
                  name: throw-dice
                restartPolicy: Never
    ```

* updated `job` definition to increase `spec.backoffLimit` from default of **6** to **10**

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
        name: throw-dice-job
    spec:
        completions: 1
        template:
            metadata:
                name: throw-dice-pod
            spec: 
                containers:
                - image: kodekloud/throw-dice
                  name: throw-dice
                restartPolicy: Never
        backoffLimit: 10
    ```

* updated `job` to *run as many times required* for **three** `completions`

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
        name: throw-dice-job
    spec:
        completions: 3
        template:
            metadata:
                name: throw-dice-pod
            spec: 
                containers:
                -  image: kodekloud/throw-dice
                    name: throw-dice
                restartPolicy: Never 
    ```

    **`sample output`**

    ```bash
    🚀  kubernetes-zero-to-pro ➜ kc get pods
    NAME                   READY   STATUS      RESTARTS   AGE
    throw-dice-job-2hf2r   0/1     Completed   0          119s
    throw-dice-job-4zt5w   0/1     Completed   0          96s
    throw-dice-job-8mljc   0/1     Completed   0          2m23s
    throw-dice-job-k4m2g   0/1     Error       0          2m13s
    throw-dice-job-lwfpl   0/1     Error       0          2m17s
    throw-dice-job-qbmzl   0/1     Error       0          110s
    throw-dice-job-rjz54   0/1     Error       0          114s
    throw-dice-pod         0/1     Error       0          38m
    ```

    **notice** the time it took to run the `job` and the number of `pods` that were created

* optimize the `job` to run **three** `jobs` in `parallel`

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
        name: throw-dice-job
    spec:
        completions: 3
        parallelism: 3
        template:
            metadata:
                name: throw-dice-pod
            spec: 
                containers:
                -  image: kodekloud/throw-dice
                    name: throw-dice
                restartPolicy: Never 
    ```

    **`sample output`**

    ```bash
    🚀  kubernetes-zero-to-pro ➜ kc get pods
    NAME                   READY   STATUS      RESTARTS   AGE
    throw-dice-job-6ct7x   0/1     Completed   0          59s
    throw-dice-job-6jf9n   0/1     Completed   0          59s
    throw-dice-job-p47j7   0/1     Completed   0          51s
    throw-dice-job-vjcjw   0/1     Error       0          59s
    throw-dice-job-zfhq6   0/1     Error       0          55s
    ```

<br>

[↩️](../)
