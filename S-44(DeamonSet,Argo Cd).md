# DeamonSet
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

## Run the **DaemonSet.yaml** file (create the DaemonSet, Namespace, and Service files).
```
kubectl create -f deamon.yml
```
<img width="652" height="176" alt="image" src="https://github.com/user-attachments/assets/9659b77c-31dd-4d19-ab7b-e89314160172" />

-----------------------------
## Verify Namespace
```
kubectl get ns
```
<img width="607" height="248" alt="image" src="https://github.com/user-attachments/assets/849dd713-8633-4a5e-b893-825b67e54dec" />

-----------------------------
## Verify how many pods are running in carrer.
```
kubectl get po -n carrer
```
<img width="645" height="152" alt="image" src="https://github.com/user-attachments/assets/9fb1f854-9a97-4dde-91e5-fb13a11a0bf1" />

--------------------------------

# Argo CD
### What Is Argo CD?
Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.
### Why Argo CD?¶
Application definitions, configurations, and environments should be declarative and version controlled. Application deployment and lifecycle management should be automated, auditable, and easy to understand.

---
## INSTALL HELM (HELM = apt):
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 
chmod 700 get_helm.sh
./get_helm.sh
helm version
```
<img width="1602" height="307" alt="image" src="https://github.com/user-attachments/assets/5408c42b-e77e-417b-bf7d-2d5c52bf25ff" />

---
## INSTALL ARGO CD USING HELM:
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl get all -n argocd
```
<img width="1242" height="418" alt="image" src="https://github.com/user-attachments/assets/1d8e2d67-abb2-4bcc-b89d-14f31743713c" />

---
## EXPOSE ARGOCD SERVER:
```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
apt install jq -y
export ARGOCD_SERVER='kubectl get svc argocd-server -n argocd -o json | jq --raw-output '.status.loadBalancer.ingress[0].hostname''
echo $ARGOCD_SERVER
kubectl get svc argocd-server -n argocd -o json | jq --raw-output .status.loadBalancer.ingress[0].hostname
```
<img width="1572" height="337" alt="image" src="https://github.com/user-attachments/assets/d204141b-dfea-404d-bcae-6a4d3d9140fb" />

--------
## Find load balancer URL to access ARGO CD
```
kubectl get svc -n argocd
```
<img width="1882" height="523" alt="image" src="https://github.com/user-attachments/assets/c8a54adb-1e70-46a5-9956-1fb39caca76f" />

--------
### Copy the load balancer URL and paste it into your browser to access Argo CD.
<img width="1915" height="990" alt="image" src="https://github.com/user-attachments/assets/5ae88ae4-fb9b-4d28-a8ac-a1cab8a74735" />

-----------
###  TO GET ARGO CD PASSWORD:
```
export ARGO_PWD='kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d'
echo $ARGO_PWD
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
<img width="1872" height="197" alt="image" src="https://github.com/user-attachments/assets/62394520-54b3-4484-b489-831ce5b78e08" />

#### User Name= admin(default)

#### Password = using above command you will get
<img width="1917" height="968" alt="image" src="https://github.com/user-attachments/assets/935f4397-bc9b-459f-b0db-0389c8c6d5c1" />

-----------
## create Deployment using Argo Cd

### Click on New
<img width="1518" height="485" alt="image" src="https://github.com/user-attachments/assets/493b8c53-a448-4d26-b1f1-bea19c89e0e6" />

<img width="1532" height="656" alt="image" src="https://github.com/user-attachments/assets/e6d534a0-0215-439b-9f95-5f957470c446" />

<img width="1556" height="478" alt="image" src="https://github.com/user-attachments/assets/61defb0e-5aa4-458e-a11e-88792f483a69" />

<img width="1568" height="532" alt="image" src="https://github.com/user-attachments/assets/b9c1a5ad-12e4-400b-96bf-b3f36e0f824d" />

<img width="1585" height="406" alt="image" src="https://github.com/user-attachments/assets/57e23e86-5ca4-4381-936c-678904434049" />

### Click on create
<img width="1916" height="922" alt="image" src="https://github.com/user-attachments/assets/710f0ffa-c33c-4ba3-9980-eab73fac272a" />
<img width="1918" height="925" alt="image" src="https://github.com/user-attachments/assets/a1f4a8c8-9523-4804-a93b-f853404c2372" />

----

## When I change my deployment file, it will automatically replicate.
#### Before
<img width="1352" height="311" alt="image" src="https://github.com/user-attachments/assets/a32be037-7c3d-4649-beb5-afcfcca7bf23" />

#### Before ( replicas: 7 change into   replicas: 3 )
<img width="1192" height="601" alt="image" src="https://github.com/user-attachments/assets/6c3e1288-ba76-43a5-8b9e-f196ad52926c" />

#### After
<img width="1052" height="602" alt="image" src="https://github.com/user-attachments/assets/75cfbf87-e6d7-4bba-ae55-f68fc0bafc78" />










