<img width="651" height="373" alt="image" src="https://github.com/user-attachments/assets/85fb9a3d-5a6d-4b0b-9e3a-7a8e8dc33ecb" />

**Kubernetes Architecture has 2 Types of Nodes:**
1. Master Node
2. Worker Node


## Master Node Server Components

**Master Node Server has 4 Types of Components:**
1. API Server
2. Controller Manager (`kube-controller-manager`)
3. Scheduler (`kube-scheduler`)
4. ETCD

---

## Client

- The person who is managing Kubernetes
- The person who is interacting with Kubernetes is called the **Client**

---

## Master Node Components Explanation

### 1. API Server
- Acts as a bridge between:
  - Client ↔ Master Components
  - Component ↔ Component

---

### 2. Controller Manager (`kube-controller-manager`)
- Helps in **recreation of Pods**
- Controller Manager has 2 types:
  1. Replication Controller Manager (for Master Node)
  2. Node Controller Manager (for Worker Node)

---

### 3. Scheduler (`kube-scheduler`)
- Schedules the right Pod on the right Worker Node

---

### 4. ETCD
- Stores cluster data such as:
  - Number of Pods
  - Number of Nodes
- Data is stored in **Key-Value pair format**

---

## Worker Node Server Components

**Worker Node Server has 3 Types of Components:**
1. Kubelet
2. Kube-Proxy
3. Pods

> By default, Worker Node runs container workloads (Docker/Container Runtime)

---

### 1. Kubelet
- Sends Worker Node information to API Server, such as:
  - Number of Pods
  - CPU usage
  - RAM usage
  - Overall node status

---

### 2. Kube-Proxy
- Handles **networking** inside the cluster

---

### 3. Pods
- A Pod is a **group of containers**

### How to Setup K8S Cluster: 
## Rerequirements:
#### -CREATE EC2 USING AMAZON-LINUX-AMI WITH 25 GB EBS AND INSTANCE_TYPE BE M7I-FLUX.LARGE(Eg: 2 CPUS,  4GB RAM),
#### -CREATE IAM ROLE WITH ADMIN ACCESS ADD THE ROLE TO YOUR  EC2 SERVER

====================================================================

#### curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s   https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
#### chmod +x kops
#### sudo mv kops /usr/local/bin/kops
#### kops version

# Explanation 
## 1️⃣ Download the latest kops binary
```
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
```

👉 What’s happening here:

- Inner curl hits GitHub API and fetches the latest kops release tag

- grep tag_name | cut ... extracts the version (for example: v1.29.x)

- Outer curl -Lo kops downloads the Linux amd64 binary

- File is saved locally as kops

This ensures you always install the latest stable version (best practice).

## 2️⃣ Make the binary executable
```
chmod +x kops
```

👉 This gives execute permission to the kops binary
Without this, Linux won’t allow you to run it.

## 3️⃣ Move kops to a global PATH location
```
sudo mv kops /usr/local/bin/kops
```

👉 Why /usr/local/bin?

It’s already part of the system $PATH

You can run kops from any directory

Standard practice for CLI tools

## 4️⃣ Verify kops installation
```
kops version
```

👉 Expected output:
You should see something like:

Version 1.xx.x (git-xxxxx)

If you see the version → ✅ kops is installed correctly

<img width="1903" height="777" alt="image" src="https://github.com/user-attachments/assets/38c14960-2c49-4bde-b249-616e2d5521ef" />


====================================================================

#### curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
#### chmod +x kubectl
#### mv kubectl /usr/local/bin/
#### kubectl version

## (This set of commands downloads, installs, and verifies kubectl, the Kubernetes command-line tool used to interact with Kubernetes clusters (EKS, kOps, kubeadm, etc.).

# Explanation 
## 1️⃣ Download the latest stable kubectl binary
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
- Explanation:
- curl → Downloads data from a URL
-L → Follows redirects
-O → Saves the file with the same name as in the URL (kubectl)
Inner curl:
Reads the latest stable Kubernetes version from stable.txt
Example output: v1.30.x
linux/amd64/kubectl → Downloads kubectl for Linux 64-bit

### 📌 Result:
Latest stable kubectl binary is downloaded to the current directory.

## 2️⃣ Give execute permission
```
chmod +x kubectl
```
Explanation:
Adds execute permission to the kubectl binary
Required to run it as a command
## 📌 Without this, Linux will block execution.

## 3️⃣ Move kubectl to system PATH
```
mv kubectl /usr/local/bin/
```
Explanation:
Moves kubectl to /usr/local/bin
This directory is already part of the system $PATH
## 📌 Benefit:
You can run kubectl from any directory.
⚠️ In most systems this should be:
sudo mv kubectl /usr/local/bin/
## 4️⃣ Verify kubectl installation
```
kubectl version
```
Explanation:
Confirms kubectl is installed
Shows client and server version (server appears only if a cluster is connected)
## 📌 Recommended check:
kubectl version --client

<img width="1910" height="777" alt="image" src="https://github.com/user-attachments/assets/b701a51e-733e-44ad-a413-add03bfb9e1c" />


====================================================================
```
aws s3 mb s3://rajesh.k8s.locals
aws s3api put-bucket-versioning --bucket rajesh.k8s.locals --region ap-south-1 --versioning-configuration Status=Enabled
export KOPS_STATE_STORE=s3://rajesh.k8s.locals
```

### Create S3 bucket for kOps state store
aws s3 mb s3://rajesh.k8s.locals

### Enable versioning on the S3 bucket
aws s3api put-bucket-versioning \
  --bucket rajesh.k8s.locals \
  --region ap-south-1 \
  --versioning-configuration Status=Enabled
##### -Protects data from accidental deletion by keeping previous versions
##### -Prevents data loss from overwrites by storing multiple object versions
##### -Enables rollback and recovery, especially critical for kOps state store
##### -Required for S3 replication (CRR / SRR) and disaster recovery
##### -Helps with compliance and auditing by maintaining object history

### Set kOps state store environment variable
export KOPS_STATE_STORE=s3://rajesh.k8s.locals
<img width="1697" height="255" alt="image" src="https://github.com/user-attachments/assets/0540e370-1679-4eb8-9d26-4464265ee2e6" />
<img width="1901" height="682" alt="image" src="https://github.com/user-attachments/assets/9730f293-b0f6-4631-9f6c-93409cc1a130" />

====================================================================
## This command creates a Kubernetes cluster configuration using kOps on AWS
```
kops create cluster --name=rajesh33.k8s.local --zones=ap-northeast-3a --control-plane-size=m7i-flex.large --control-plane-count=1 --node-count=2 --node-size=t3.micro --image=ami-06571d6ae17e327ff
```
<img width="1882" height="637" alt="image" src="https://github.com/user-attachments/assets/14cba679-c5ee-4ab3-9220-b603c1854e16" />

## update cluster
```
kops update cluster --name rajesh33.k8s.local --yes --admin
```


====================================================================
## Delete  a cluster
### 1. export 
```
export KOPS_STATE_STORE=s3://rajesh.k8s.locals
```
### 2. kops delete 
```
kops delete cluster --name rajesh33.k8s.local --yes
```
==================================================================
