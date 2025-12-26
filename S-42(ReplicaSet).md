# ReplicationController
### In Kubernetes, when a Pod is deleted, it is not recreated automatically. To overcome this limitation, the ReplicationController was introduced.
_________________
## ReplicationController 

ReplicationController is one of the basic and older concepts in Kubernetes. Its main job is very simple — **to make sure a fixed number of pods are always running.
**
Think of it like a **watchman** for your pods.
If any pod goes down for any reason, ReplicationController immediately creates a new one so that your application stays up.
________________

## Why ReplicationController is Needed

In a real environment, pods are not permanent. They can:

--- Crash
--- Get deleted by mistake
--- Go down if a node fails

ReplicationController handles all this automatically.
You don’t have to sit and monitor pods manually.

Example:

--- You want 3 pods running

--- One pod crashes

--- ReplicationController notices this and creates a new pod automatically

So your application continues to run without downtime.

________________

## What ReplicationController Actually Does

ReplicationController continuously checks two things:

--- How many pods should be running

--- How many pods are currently running

If both numbers don’t match, it takes action.

--- Less pods? ➝ Create new pods

--- More pods? ➝ Remove extra pods

Simple logic, but very powerful.

________________

## Important Parts of ReplicationController

A ReplicationController mainly has three parts:

**--- replicas**

Number of pod copies you want

**--- selector**

Used to identify which pods belong to this controller

**--- template**

________________

## What Happens If a Pod Is Deleted?

Let’s say you manually delete a pod:
```
kubectl delete pod <pod-name>
```

**What happens next?**

ReplicationController immediately detects the pod count is reduced

It **creates a new pod automatically**

No manual work. Kubernetes handles it for you.

________________

## Scaling Pods Using ReplicationController

You can increase or decrease pod count easily.

Using command line:
```
kubectl scale rc my-rc --replicas=5
```

This will scale your application from 3 pods to 5 pods.
________________

### Limitations of ReplicationController

This is important to understand.

--- It does not support rolling updates

--- Selector options are very limited

--- It is considered legacy now

Because of these limitations, ReplicationController is **rarely used in modern Kubernetes setups.**

### What Do We Use Instead?

In today’s real-world projects:

--- Deployment is used

--- Deployment internally manages ReplicaSets

--- ReplicaSets are the improved version of ReplicationController
_________________________




## What is a ReplicaSet in Kubernetes (K8s)?

A **ReplicaSet** is a Kubernetes object that ****ensures a specified number of identical Pods are always running.**

👉 In simple words:
**ReplicaSet = Pod count manager**

-----------------------------------------
## Why do we need a ReplicaSet?

Imagine this situation:

--- You want **3 Pods** of your application running

--- One Pod crashes or gets deleted accidentally

💡 **ReplicaSet automatically creates a new Pod** to maintain the desired count.

So it gives you:

✅ High availability

✅ Self-healing

✅ Consistency

--------------------------------------

## How ReplicaSet works (real-time example)

If you define:
```
replicas: 3
```

ReplicaSet will ensure:

---- If 1 Pod goes down → a new Pod is created

---- If someone manually deletes a Pod → ReplicaSet recreates it

---- If Pods become 4 → ReplicaSet deletes extra Pods

🎯 It **strictly maintains the desired number of Pods**

--------------------------------------
# Create ReplicaSet in Kubernetes
```
vim myrs.yml
```
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myrs1
  labels:
    app: cycle
spec:
  replicas: 7
  selector:
    matchLabels:
      app: cycle
  template:
    metadata:
      labels:
        app: cycle
    spec:
      containers:
      - name: con1
        image: shammu101/cycle
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: mysvc1
spec:
  type: LoadBalancer
  selector:
    app: cycle
  ports:
  - port: 80
    targetPort: 80
```
<img width="1102" height="623" alt="image" src="https://github.com/user-attachments/assets/6b02fa33-664f-4bfa-8d78-349cff1d62ae" />


----------------------
### Create the Pod and Service Files
```
kubectl create -f myrs.yml
```
<img width="827" height="171" alt="image" src="https://github.com/user-attachments/assets/2a41f509-e040-42d1-9a10-4cd982a9b403" />

----------------------
### Verify Get both Pods and Services
```
kubectl get pods,svc
```
<img width="1731" height="396" alt="image" src="https://github.com/user-attachments/assets/8388b7ab-cd7f-42ac-99c0-c40fc2d9e7ed" />

----------------------
### Delete the Pod and verify whether it is recreated automatically.
```
kubectl delete pod --all
```

<img width="721" height="631" alt="image" src="https://github.com/user-attachments/assets/9c76c6a1-d47b-4cc9-931b-bf86f75958a9" />

----------------------

<img width="1918" height="917" alt="image" src="https://github.com/user-attachments/assets/8b693153-d68f-48a5-bba7-cf8dabe17c4e" />



