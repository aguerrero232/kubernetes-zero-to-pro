# Kubernetes - **Replication Controllers** and ***Replica Sets***


### ***Replica Sets are newer than Replication Controllers, and are the preferred way to manage pods!***



<br>

**Examples of simple Replication Controller and Replica set are defined in the yaml files included in this directory**


<br>

- A Replica Set is a set of pods that are managed by a controller
- Ensures that the specified number of pods are running at any given time
- If a pod fails, the Replica Set will create a new one to replace it


<br>

___

<br>

## Why use Replica Sets?

* Process to monitor pods, by labeling pods it will allow replica set to know which pods to monitor and provides a method to filter out pods thats are not part of the replica set

<br>

___

<br>

## ***Basic Commands***

* create a replica set 
    ```
    kubectl create -f <yaml file>
    ```

* get list of replica sets
    ```
    kubectl get replicaset
    ```

* get descriptive information on the desired replica set
    ```
    kubectl describe replicaset <replica set name>
    ```

* edit the specified replica set
    ```
    kubectl edit replicaset <replica set name>
    ```

* scale replica set to the desired number of replicas

    ```
    kubectl replace -f <edited yaml file>
    ```

    ```
    kubectl scale --replicas=<new number of replicas> -f <yaml file>
    ```


* delete specified replica set

    ```
    kubectl delete replicaset <replica set name>
    ```
