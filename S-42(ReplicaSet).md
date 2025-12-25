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
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
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
        image: nginx:latest
        ports:
        - containerPort: 80

```
