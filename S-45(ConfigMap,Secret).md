# ConfigMap 
## What is a ConfigMap in Kubernetes?

A **ConfigMap** is used to **store non-confidential configuration data** like:

--- Environment variables

--- Application configs

--- Properties files

--- Key–value pairs

👉 This data is **separate from the application code and container image.**

------------------------------

## Why do we need ConfigMaps?

Imagine this ❌ (bad practice):

--- Hardcoding DB URL, app name, port inside Docker image

--- For every change → rebuild image → redeploy

With ConfigMaps ✅:

--- Change config **without rebuilding image**

--- Same image can run in **dev / test / prod**

--- Clean separation of code and config

------------------------------
#### **Interview One-Liner 🧠**

“A ConfigMap is used to store non-sensitive configuration data and inject it into Pods as environment variables or files.”

------------------------------

## What kind of data goes into ConfigMaps?

✔ App name
✔ Environment name
✔ Ports
✔ URLs
✔ Feature flags

⚠️ **NOT for passwords or secrets**
(use **Secrets** for that)

-------------------------
## Create a ConfigMap File
```
vim configmap.yml
```
```
apiVersion: apps/v1
kind: ConfigMap
metadata:
  name: my-config
data:
  DATABASE_URL: "postgress://user:password@hostname:5432/dbname"
  REDIS_HOST: "redis-server"
  REDIS_PORT: "6379"
  APP_MODE: "production"
  NAME: "rajesh" 
  PLACE: "hyd"
```
<img width="996" height="452" alt="image" src="https://github.com/user-attachments/assets/51aec535-f476-40bd-80a8-6b9363eac089" />

------------------------
### Create the Pod and Service Files
```
kubectl create -f pod.yaml -f service.yaml
```
<img width="837" height="150" alt="image" src="https://github.com/user-attachments/assets/a9ce44ae-f207-47dc-a1e6-4d19ee118574" />

----------------------
### Verify Get both Pods and Services
```
kubectl get pods,svc
```
<img width="1098" height="315" alt="image" src="https://github.com/user-attachments/assets/e487eb23-7fbb-426e-bce0-bf2c2d5eb95d" />

