# Kubernetes Ingress 

In Kubernetes, **Ingress** is used to **expose HTTP and HTTPS applications to the outside world.**

**Ingress provides external access to services using URLs and domains, instead of ports.**

It acts like a **smart entry gate** for your cluster.

---------------------------
## Why Do We Need Ingress?

Before Ingress, we used:

* NodePort ❌ (ugly port numbers)

* LoadBalancer ❌ (one LB per service = expensive)

Ingress solves this problem.

With Ingress:

* One Load Balancer

* Multiple applications

* Access using **domain names and paths**
  
--------------------
## Real-World Example

**Without Ingress:**

app1 → NodeIP:30001
app2 → NodeIP:30002


**With Ingress:**

app1 → example.com/app1
app2 → example.com/app2

-----------------------------

## How Ingress Works

Ingress itself does **NOT work alone.**

You need **three components:**

1. **Deployment** (your app)

2. **Service** (exposes pods internally)

3. **Ingress + Ingress Controller**

=> Ingress Controller is the actual engine.

Common controllers:

* NGINX Ingress Controller (most popular)

* AWS ALB Ingress Controller

* Traefik
----------------------------------
## Path-Based Routing Example
/example → app1-service
/admin   → app2-service

One domain, multiple apps.

-----------------------------
## Host-Based Routing Example
app1.example.com → app1-service
app2.example.com → app2-service

Very common in production.

-----------------------------
## When to Use Ingress

Use Ingress when:

* You have multiple services

* Need domain-based access

* Want HTTPS

* Want cost-effective solution
* 
--------------------------------
## When NOT to Use Ingress

Avoid Ingress when:

* Simple testing

* Single app only

* No domain required

Then NodePort or LoadBalancer is fine.

------------------------------
**Ingress is a Kubernetes resource used to expose multiple services externally using HTTP/HTTPS with domain and path-based routing.**

--------------------------------------
<img width="1115" height="732" alt="image" src="https://github.com/user-attachments/assets/07c03557-e8bc-40d2-be56-35e25bbc4522" />

----------------------------------------
## Install NGINX Ingress Controller
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.1/deploy/static/provider/cloud/deploy.yaml
```
<img width="1857" height="537" alt="image" src="https://github.com/user-attachments/assets/0b7cbf81-30a5-454e-8903-7041fc0ea3c6" />

----------------------------------------
## Create Pods
```
vim dep.yml
```
```
apiVersion: apps/v1
kind: Deployment
matadata:
  name: mydep12
  labels:
    app: dm
spec:
  replicas: 4
  selector:
    matchLabels:
      app: dm
  template:
    metadata:
      labels:
        app: dm
    spec:
      containers:
        - name: cont12
          image: shammu101/dm
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
    app: dm
  ports:
    - port: 80
      targetPort: 80
      nodePort: 31000
---
apiVersion: apps/v1
kind: Deployment
matadata:
  name: mydep11
  labels:
    app: cycle
spec:
  replicas: 4
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
  name: mysvc44 
spec:
  type: NodePort
  selector:
    app: cycle
  ports:
    - port: 80
      targetPort: 80
      nodePort: 32000
```
<img width="1171" height="631" alt="image" src="https://github.com/user-attachments/assets/e5dc1b91-4c72-47db-a803-93f877423cab" />
