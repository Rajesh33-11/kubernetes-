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
### Verify a configmap
```
kubectl get configmap
```
<img width="736" height="232" alt="image" src="https://github.com/user-attachments/assets/2974b634-7933-47e5-a26d-bb75d6b91f5f" />

----------------------

## Create a Deployment File (ConfigMap)
```
vim dep.yml
```
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
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
          env:
            - name: DATABASE_URL
              valueFrom:
                configMapKeyRef:
                  name: my-config
                  key: DATABASE_URL
            - name: REDIS_HOST
              valueFrom:
                configMapKeyRef:
                  name: my-config
                  key: REDIS_HOST
            - name: REDIS_PORT
              valueFrom:
                configMapKeyRef:
                  name: my-config
                  key: REDIS_PORT
            - name: APP_MODE
              valueFrom:
                configMapKeyRef:
                  name: my-config
                  key: APP_MODE
```
<img width="1090" height="582" alt="image" src="https://github.com/user-attachments/assets/05835e19-7626-459a-8c60-988fb04e5152" />


------------------------
### Create the dep file
```
kubectl create -f dep.yml
```
<img width="1046" height="185" alt="image" src="https://github.com/user-attachments/assets/a2b945b8-7723-425a-a444-6c885527ef4b" />

----------------------
### Verify a Deployment
```
kubectl get deployment
```
<img width="822" height="182" alt="image" src="https://github.com/user-attachments/assets/c0f2c169-128d-4af0-b63f-4c4a00489c68" />

----------------------
### Verify a Replicaset
```
kubectl get rs
```
<img width="806" height="142" alt="image" src="https://github.com/user-attachments/assets/cc47a28c-1016-4b53-913f-fc9809a85f27" />

----------------------
### Verify a Pods
```
kubectl get po
```
<img width="953" height="211" alt="image" src="https://github.com/user-attachments/assets/2f4006e8-0838-4793-996f-ec9ef8965857" />

----------------------
### Print a Data Using grep command
i want print database url
(kubectl exec pod_id -- printenv | grep DATABASE_URL)
```
kubectl exec nginx-deployment-68845b6759-rcdqm -- printenv | grep DATABASE_URL
```
<img width="1251" height="215" alt="image" src="https://github.com/user-attachments/assets/985b55f4-b140-42a2-86f6-236eff18de51" />

----------------------
