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
<center><h3>Ingress vs Service (Important Difference)</h3></center>
Feature	Service	Ingress
Exposes pods	✅	❌
Load balancing	✅	❌
URL routing	❌	✅
Domain support	❌	✅
SSL termination	❌	✅

👉 Ingress sits on top of Services.

SSL / HTTPS with Ingress

Ingress supports HTTPS using TLS.

Example:

tls:
- hosts:
  - myapp.example.com
  secretName: tls-secret


Ingress handles:

SSL termination

HTTPS traffic

Ingress Controller Is Mandatory ⚠️

Very important interview point:

Creating an Ingress resource without an Ingress Controller does NOTHING.

Ingress Controller examples:

NGINX

AWS ALB

GKE Ingress

When to Use Ingress

Use Ingress when:

You have multiple services

Need domain-based access

Want HTTPS

Want cost-effective solution

When NOT to Use Ingress

Avoid Ingress when:

Simple testing

Single app only

No domain required

Then NodePort or LoadBalancer is fine.

One-Line Interview Answer 🎯

Ingress is a Kubernetes resource used to expose multiple services externally using HTTP/HTTPS with domain and path-based routing.
