# 🔴 4xx Errors – Client Side Errors (Your mistake)
## 403 – Forbidden ❌

### Meaning:
👉 You are trying to access something, but you don’t have permission

## Common AWS reasons:

-- IAM user doesn’t have required policy

-- S3 bucket/object is private

-- Security Group / NACL blocking access

-- CloudFront + S3 → bucket policy missing

-- WAF blocking your IP

### Example:

-- Opening S3 object URL → 403

-- Accessing EC2 page → 403

#### How to solve (simple checklist):

✔ Check IAM permissions
✔ Check S3 bucket policy & object ACL
✔ Check Security Group inbound rules
✔ Check WAF rules (if used)

### 💡 Interview line:

“403 means authentication is successful, but authorization is missing.”

--------------------
## 404 – Not Found ❓

#### Meaning:
👉 Resource does not exist

### Common reasons:

-- Wrong URL

-- File deleted

-- Wrong path in ALB / CloudFront

-- Static website index file missing

### How to solve:

✔ Verify URL
✔ Check file exists (S3 / EC2 path)
✔ Check ALB target path

# 🔴 5xx Errors – Server Side Errors (AWS / Application problem)
## 500 – Internal Server Error 💥

### Meaning:
👉 Server got the request but application failed

#### Common AWS reasons:

-- Application crash (Java, Node, PHP)

-- Wrong config file

-- Database connection failed

-- Environment variable missing

### How to solve:

✔ Check application logs
✔ Restart service (httpd, nginx, app)
✔ Check DB connectivity
✔ Check IAM role for app

---------------------------------------
## 502 – Bad Gateway 🔁

### Meaning:
👉 Load Balancer got bad response from backend

## Common AWS reasons:

-- EC2 instance is down

-- App not running on expected port

-- Wrong target group port

-- Health check failing

How to solve:

✔ Check Target Group health
✔ Verify app is running
✔ Verify port number
✔ Check security group between ALB ↔ EC2

------------------------
## 503 – Service Unavailable 🚫

### Meaning:
👉 Server is temporarily unavailable

#### Common AWS reasons:

-- No healthy targets in ALB

-- Auto Scaling launching new instances

-- Server overloaded (CPU/RAM 100%)

-- Maintenance or deployment time

### How to solve:

✔ Check Target Group → Healthy/Unhealthy
✔ Check EC2 CPU & Memory
✔ Scale instances (ASG)
✔ Check deployment status

## 💡 Real-time example:
When ASG replaces instances → 503 happens for few seconds

### 🔥 Quick Exam + Interview Summary (VERY IMPORTANT)
Error        	Who is wrong?	                   Simple Meaning
403             	User	                      Permission problem
404              	User	                      Resource not found
500	              Server                    	App crashed
502	              Server	                    LB ↔ Backend issue
503	              Server	                    Service down / overloaded

-----------------------------

## One golden troubleshooting rule 🧠

### 👉 4xx → Check IAM, URL, permissions
### 👉 5xx → Check EC2, ALB, App, Logs
