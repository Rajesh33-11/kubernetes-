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
<img width="1657" height="657" alt="image" src="https://github.com/user-attachments/assets/4e029724-1cb7-43be-ad6c-4d29e3611939" />

<img width="1556" height="478" alt="image" src="https://github.com/user-attachments/assets/61defb0e-5aa4-458e-a11e-88792f483a69" />

<img width="1602" height="557" alt="image" src="https://github.com/user-attachments/assets/4d7bb07c-31fd-42d1-8e34-8a3c040e0cfc" />


<img width="1572" height="442" alt="image" src="https://github.com/user-attachments/assets/a61b9b78-d5f0-4a7e-b637-3de876694f3e" />


### Click on create
<img width="1918" height="975" alt="image" src="https://github.com/user-attachments/assets/8bca52f6-d91b-46ff-941c-86e1805cfbe0" />
<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/40359657-1034-42f1-819e-1bb3a997d69d" />

----

## When I change my deployment file, it will automatically replicate.
#### Before
<img width="911" height="298" alt="image" src="https://github.com/user-attachments/assets/224b065f-743f-405b-9bfb-5955b163e01a" />



#### Before ( replicas: 7 change into   replicas: 3 )
<img width="1272" height="660" alt="image" src="https://github.com/user-attachments/assets/79a5931b-0761-409f-80c1-6fc40ef3132e" />


#### After
<img width="960" height="591" alt="image" src="https://github.com/user-attachments/assets/41a9294a-014f-4e3f-82a8-6a78efaf9047" />

#### After
<img width="942" height="422" alt="image" src="https://github.com/user-attachments/assets/816e168e-1d03-4938-b248-d6e1edf52597" />



