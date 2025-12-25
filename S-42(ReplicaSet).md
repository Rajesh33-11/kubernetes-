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
  name: myrs
  lables:
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
-------

apiVersion: v1
kind: Service
metadata:
  name: mysvc
spec:
  type: LoadBalancer
  selector:
    app: cycle
  ports:
    - port: 80      
      targetPort: 80 
```
<img width="1312" height="625" alt="image" src="https://github.com/user-attachments/assets/8d909de6-0180-4c8b-9799-3210317d863d" />

----------------------
### Create the Pod and Service Files
```
kubectl create -f myrs.yaml
```
<img width="807" height="162" alt="image" src="https://github.com/user-attachments/assets/03ec0837-9cdf-44e3-ae79-7e425204160e" />

----------------------
### Verify Get both Pods and Services
```
kubectl get pods,svc
```
<img width="1740" height="257" alt="image" src="https://github.com/user-attachments/assets/de0dbcab-b618-4a14-89bf-69194b8df342" />
