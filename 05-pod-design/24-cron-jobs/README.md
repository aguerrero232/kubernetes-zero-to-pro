# <img src="../../00-resources/img/k8s.png" width="30px"> **Kubernetes** - ***CronJobs*** ⏳

## **Description** 👀

`CronJobs` are a way to *schedule a job to run at a **specific time** or **interval***.  `CronJobs` are a *great way to automate tasks* that need to be **run on a regular basis**. `CronJobs` are *similar to `Jobs`* but have a **schedule** instead of a **trigger**.

<br />

## **Examples** 🧩

* sample `CronJob` definition

    ```yaml
    apiVersion: batch/v1
    kind: CronJob
    metadata:
        name: math-add-cronjob
    # spec for the cron job
    spec:
        # schedule is a cron expression, in this case it will run every minute
        schedule: "*/1 * * * *"
        jobTemplate:
            # spec for the job that will be created
            spec:
                template:
                # spec for the pod that will be created
                spec:
                    containers:
                    - name: math-add
                        image: ubuntu
                        command: ["expr", "77", "+", "5"]
                    restartPolicy: Never
    ```

* `CronJob` for the **example** used in the [`Jobs`](/05-pod-design/23-jobs/README.md) section to run at **21 hours 30 minutes everyday**

    ```yaml
    apiVersion: batch/v1
    kind: CronJob
    metadata:
        name: throw-dice-cron-job
    spec:
        schedule: "30 21 * * *"
        jobTemplate:
            spec:
                completions: 3
                parallelism: 3
                template:
                    metadata:
                        name: throw-dice-pod
                    spec:
                        containers:
                        - image: kodekloud/throw-dice
                            name: throw-dice
                        restartPolicy: Never
    ```

<br>

[↩️](../README.md)
