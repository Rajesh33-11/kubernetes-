o```
apiVersion: apps/v1
kind: ReplicaSet
matadata:
  name: myrs
  labels:
    app: cycle
spec:
  replicas: 9
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
  name: mysvc
spec:
  selector:
    app: cycle
  ports:
    - port: 80
      targetPort: 80
      nodePort: 31000
```


```
apiVersion: apps/v1
kind: Deployment
matadata:
  name: mydep1
  labels:
    app: cycle
  namespace: dev-env
spec:
  replicas: 9
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
  name: mysvc
  namespace: dev-env
spec:
  type: LoadBalancer
  selector:
    app: cycle
  ports:
    - port: 80
      targetPort: 80
      nodePort: 31000
```
