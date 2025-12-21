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
apiVersion: v1
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
<img width="1003" height="418" alt="image" src="https://github.com/user-attachments/assets/aa373758-0ad4-4f1f-b847-60a6c0c3c923" />

------------------------
### Create the configmap
```
kubectl create -f configmap.yml
```
<img width="817" height="141" alt="image" src="https://github.com/user-attachments/assets/6d03c992-e852-43b4-ab39-ad15890d0c58" />

----------------------
### Verify Get configmap
```
kubectl get configmap
```
<img width="736" height="232" alt="image" src="https://github.com/user-attachments/assets/2974b634-7933-47e5-a26d-bb75d6b91f5f" />


