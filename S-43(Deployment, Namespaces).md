## Kubernetes Deployment 
A Deployment is one of the most important and commonly used objects in Kubernetes.
In real-world projects, **Deployment is what we use to run applications.**
In simple terms:

**Deployment manages ReplicaSets, and ReplicaSets manage Pods.**

You don’t directly worry about pods anymore — you define the desired state, and **Deployment takes care of everything.**

----------------------

## Why Do We Need Deployment?
Before Deployment, we had:

* ReplicationController
* ReplicaSet

They could maintain pod count, but they had **major limitations:**

* No rolling updates
* No rollback
* Risk of downtime during updates


Deployment solves all these problems.

----------------------
## What Deployment Does for You
A Deployment handles:


Creating pods


* Maintaining required replicas


* Updating application versions


* Rolling updates (zero downtime)


* Rollback to previous versions


* Scaling pods up or down


That’s why Deployment is production-ready.

----------------------
## Basic Deployment YAML File
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```

----------------------
Explanation 
## 1. apiVersion & kind
```
apiVersion: apps/v1
kind: Deployment
```
Tells Kubernetes:

**“I want to create a Deployment object.”**

----------------------
## 2. metadata
```
metadata:
  name: nginx-deployment
```
* Name of the Deployment
* Used for identification and management

----------------------
## 3. replicas
```
replicas: 3
```
* Number of pod copies you want
* Kubernetes ensures 3 pods are always running
----------------------
## 4. selector
```
selector:
  matchLabels:
    app: nginx
```
* Deployment uses this to identify which pods it manages
* Must match pod labels exactly
--Selector and pod labels must match, otherwise Deployment won’t work correctly.

----------------------
## 5. template
This is the pod definition.
Whatever you put here is what Kubernetes runs as a pod.
```
template:
  metadata:
    labels:
      app: nginx
```
Labels used by Deployment and Service.
```
spec:
  containers:
  - name: nginx
    image: nginx
```
Defines the container and image.

----------------------
## How Deployment Works Internally
#### This is very important :
When you create a Deployment:

* Deployment creates a **ReplicaSet**


* ReplicaSet creates **Pods**


* Deployment monitors ReplicaSet and Pods

Flow:

**Deployment → ReplicaSet → Pods**

You interact with Deployment, not ReplicaSet directly.

----------------------

## Rolling Updates - Biggest Advantage
Let’s say you update the image:
```
image: nginx:1.25
```
Deployment will:

* Create a new ReplicaSet
* Gradually bring up new pods
* Slowly terminate old pods
* Ensure **no downtime**

This is called **a rolling update.**

----------------------

## Rollback Feature (Life Saver)
If something goes wrong after deployment:
```
kubectl rollout undo deployment nginx-deployment
```
**Kubernetes rolls back to the previous stable version.**
This is something:
ReplicaSet,ReplicationController **cannot do.**

----------------------

## Scaling Deployment
You can scale easily.
Using YAML:
```
replicas: 5
```
**No downtime, no stress.**

----------------------

## Checking Deployment Status
Useful commands:
```
kubectl get deployment
kubectl describe deployment nginx-deployment
kubectl rollout status deployment nginx-deployment
kubectl rollout history deployment nginx-deployment
```

----------------------

## Deployment Strategies
By default, Deployment uses:

***RollingUpdate** (most common)

Other option:
***Recreate** (delete old pods first, then create new ones)

RollingUpdate is what we use in almost all cases.


----------------------

## When to Use Deployment
Use Deployment when:

* Running stateless applications
* Building web apps or APIs
* Need zero-downtime updates
* Want rollback capability

 Basically, **99% of applications use Deployment.**

---------------------
Deployment is a higher-level Kubernetes object that manages ReplicaSets and provides rolling updates, rollback, and scaling with zero downtime.
----------------------
# Create Deployment in Kubernetes
```
vim dep.yml
```
```
apiVersion: apps/v1
kind: Deployment
matadata:
  name: mydep11
  labels:
    app: cycle
spec:
  replicas: 9
  selector:
    matchLabels:
      app: cycle
  template:
    metadata:
      labels:
        app: cycle
    spec:
      containers:
        - name: cont1
          image: shammu101/cycle
          ports:
            - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: mysvc33 
spec:
  type: NodePort
  selector:
    app: cycle
  ports:
    - port: 80
      targetPort: 80
      nodePort: 31000
```

