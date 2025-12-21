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
kind: Deployment
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

