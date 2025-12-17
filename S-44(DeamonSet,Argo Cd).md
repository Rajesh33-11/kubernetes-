## Verfiy List of Pods
```
kubectl get Pods
```
<img width="613" height="123" alt="image" src="https://github.com/user-attachments/assets/c180f7d2-9cff-4142-94ec-3b50be11c490" />

---
## Create Pods Using DeamonSet
```
vim deamon.yml
```
```
apiVersion: v1
kind: Namespace
metadata:
  name: carrer
---
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: mydm
  namespace: carrer
  labels:
    app: dm
spec:
  selector:
    matchLabels:
      app: dm
  template:
    metadata:
      labels:
        app: dm
    spec:
      containers:
        - name: cont1
          image: shammu101/dm
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: mysvc
  namespace: carrer
spec:
  type: LoadBalancer
  selector:
    app: dm
  ports:
    - port: 80
      targetPort: 80
```
<img width="802" height="517" alt="image" src="https://github.com/user-attachments/assets/c90eaedc-0148-4b3c-bcf9-7eda8e48c5ee" />
## run DaemonSet.yml file (create deamonset, namespace and service file)
```
kubectl create -f deamon.yml
```
<img width="652" height="176" alt="image" src="https://github.com/user-attachments/assets/9659b77c-31dd-4d19-ab7b-e89314160172" />

-----------------------------
