# ArgoCD + Private Git Repo → Pod Creation
----
## Create a GitHub access token.
<img width="1053" height="430" alt="image" src="https://github.com/user-attachments/assets/25153a19-14aa-4a27-966c-c91b179704c3" />

---------------
## Add Private Repository Using Argo CD UI

#### Login to Argo CD UI
#### Go to Settings → Repositories
<img width="1914" height="867" alt="image" src="https://github.com/user-attachments/assets/9a8a0a9c-a232-408c-97f4-172b78675a5a" />

#### Click Connect Repo
<img width="1751" height="522" alt="image" src="https://github.com/user-attachments/assets/a64e6e45-dfa5-4614-b046-f20b751b625b" />

#### Select HTTPS
<img width="1901" height="447" alt="image" src="https://github.com/user-attachments/assets/073efbb2-8d53-414b-8128-c1e2156ed7ef" />

#### Fill in details:
####  Click Connect
<img width="1918" height="902" alt="image" src="https://github.com/user-attachments/assets/1e97d968-3133-420e-93c7-5dc28bf97d08" />

#### Repository status should show Successful
<img width="1916" height="502" alt="image" src="https://github.com/user-attachments/assets/3d939a4e-0911-40a0-9d73-9bc4bb9e110d" />

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
<img width="756" height="287" alt="image" src="https://github.com/user-attachments/assets/f26a7ba0-b49e-4135-bc4d-eb21eab46e85" />


#### Before ( replicas: 7 change into   replicas: 3 )
<img width="1192" height="601" alt="image" src="https://github.com/user-attachments/assets/6c3e1288-ba76-43a5-8b9e-f196ad52926c" />

#### After
<img width="1052" height="602" alt="image" src="https://github.com/user-attachments/assets/75cfbf87-e6d7-4bba-ae55-f68fc0bafc78" />

#### After
<img width="982" height="462" alt="image" src="https://github.com/user-attachments/assets/89209bf8-fd54-4877-bc0b-1ca79ac3ac6b" />


