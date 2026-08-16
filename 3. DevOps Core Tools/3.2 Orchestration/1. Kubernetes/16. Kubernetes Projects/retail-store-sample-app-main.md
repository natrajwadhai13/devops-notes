---
title: "• retail-store-sample-app-main"
parent: "16. Kubernetes Projects"
grand_parent: "• Kubernetes"
grand_grand_parent: 3. DevOps Core Tools
nav_order: 1
has_children: true
---

Aapke interview ke liye ye project kaafi useful hai, kyunki isme **Infrastructure → Container → Kubernetes → Helm → GitOps → Application deployment** complete flow dikhaya ja sakta hai.

## 1. Overall Project Architecture

![Image](https://images.openai.com/static-rsc-4/Ju_wJdsUZTEn8XS5H49znUwDmg2X3lPGk_r3ItKwOmVGNFcAXz_3a9wxj4AmTNCYWaXAoam-fqXGPaZhuESOD8u6J-OZBsEfB_i1C6RzXhSSdbkcrTQJICb1QHjaMeRPxgkrjtAOR_YElzgs3m7tpf2q6YYllveTbCSgwE_QhvYecIBoBKpOhWuWtCj9L9_Z?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Qm92OWZXBxw3R6JlpaM_q7MciVzQhXBnh1grjOb2AuxvlZxSTYZ8CwswyCcb0geYZET4O4YXZLPdXkqekBpqk_iC2vS024vjflvtu_02xCxm29PyME7RK8D1lf582y7UQ-zEnKL-EkuvqpMhq5RRnliaz-k6cX9hV0OFK_IzkInO1ulXFkrlPshJitFlC3tM?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/PULb2DoKN8P0-g8OMJ16PuR7olM-BvQl_iDYbQDDpRDZfLnhQvyOqqyURUzo59cvfNs_rRzs4jrAxULZKvEJnNHt20a7CLcbQENfT__OWJKu7B6t3jh2VknLzoRsMt21hFiCeZw0WFGvW2SaMEbaX4aKrRafna2WbYiKO08F8iyQ0RhaKIuBbFrbZ7La6xwJ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/AdmvhDf-EfJOPW0XXmTyAudaCvtriRYhMZ-cn3GLjiWFkmzM_cO9P9CTI30C7bQZAIEYt1jz79BIACk0CdeZi0zBS-S2ps-EKNcISGEDv3iqvKuxN9ZddsXst1rRMuFTtJ4yv4XvjDLi-StBjUevqmHO7EwGQCF3Eezm2zxxIaM9ZTR8457wcP2YLMhmW59i?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/6pS3_Phk2Z_-p__hYjN9TxWHms7zvUydOcMBLc87iXjisA6AZSXO9ezaQ4p5zaY5LmbfBSKFLTFPDg9MtaCBjSLj5mh-MRFevstpPagsijd9jeGNoGd5ndj_cn-GvCcjvU-xafOg5gSqfbDrzZBKqAMVIGJJeUFE_fAGF8faU2iy2qNXVkyD4lUlXChOYGMi?purpose=fullsize)

High-level flow:

```text
Developer
    |
    | Git Push
    v
GitHub Repository
    |
    +----------------------+
    |                      |
    v                      v
Application Code       Terraform
    |                      |
    v                      v
Docker Build             AWS
    |                      |
    v                      v
ECR                     VPC
                           |
                           v
                         EKS
                           |
             +-------------+-------------+
             |                           |
        Argo CD                    NGINX Ingress
             |                           |
             v                           v
       Helm Charts                 AWS NLB
             |                           |
             +-------------+-------------+
                           |
                           v
                    Retail Store UI
                           |
        +------------------+------------------+
        |         |         |        |         |
        v         v         v        v         v
     Catalog    Cart    Checkout   Orders
        |         |         |        |
        v         v         v        v
      MySQL   DynamoDB    Redis   PostgreSQL
                                  RabbitMQ
```

---

# 2. Sabse important point — ye single application nahi hai

Is project ko **5 major microservices** mein divide kiya gaya hai:

| Service  | Technology         | Purpose                      |
| -------- | ------------------ | ---------------------------- |
| UI       | Java / Spring Boot | Frontend/API gateway type UI |
| Catalog  | Go                 | Product/catalog management   |
| Cart     | Java / Spring Boot | Shopping cart                |
| Checkout | Node.js / NestJS   | Checkout processing          |
| Orders   | Java / Spring Boot | Order management             |

Aur supporting databases/services:

```text
Catalog  → MySQL
Cart     → DynamoDB
Checkout → Redis
Orders   → PostgreSQL + RabbitMQ
```

Isliye interview mein ise **microservices-based retail application** bolna better hai.

---

# 3. ZIP ka folder structure

Main repository roughly aisa hai:

```text
retail-store-sample-app-main/
│
├── README.md
├── BRANCHING_STRATEGY.md
│
├── terraform/
│   ├── main.tf
│   ├── addons.tf
│   ├── argocd.tf
│   ├── security.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── locals.tf
│   └── versions.tf
│
├── argocd/
│   ├── applications/
│   │   ├── retail-store-cart.yaml
│   │   ├── retail-store-catalog.yaml
│   │   ├── retail-store-checkout.yaml
│   │   ├── retail-store-orders.yaml
│   │   └── retail-store-ui.yaml
│   │
│   └── projects/
│       └── retail-store-project.yaml
│
├── src/
│   ├── app/
│   ├── ui/
│   ├── catalog/
│   ├── cart/
│   ├── checkout/
│   └── orders/
│
└── docs/
```

Ye structure khud hi interview mein explain karne ke liye bahut useful hai.

---

# 4. STEP 1 — Developer code push karta hai

Sabse pehle developer application code mein change karta hai.

Example:

```text
src/catalog/
src/cart/
src/checkout/
src/orders/
src/ui/
```

Suppose developer ne Catalog service mein change kiya:

```text
src/catalog/...
```

Production GitOps flow mein:

```text
Developer
   |
   | git push
   v
GitHub
   |
   v
GitHub Actions
```

GitHub Actions changed service identify karta hai.

For example:

```text
src/catalog changed
       |
       v
Build catalog Docker image
       |
       v
Push catalog image to ECR
```

---

# 5. STEP 2 — Terraform Infrastructure

Project ka infrastructure `terraform/` directory mein hai.

Important files:

```text
terraform/
├── main.tf
├── addons.tf
├── argocd.tf
├── security.tf
├── variables.tf
├── outputs.tf
├── locals.tf
└── versions.tf
```

Terraform ka main responsibility:

```text
AWS
 |
 +-- VPC
 |    |
 |    +-- Public Subnets
 |    +-- Private Subnets
 |    +-- Internet Gateway
 |    +-- NAT Gateway
 |
 +-- EKS
 |
 +-- Security Groups
 |
 +-- EKS Add-ons
 |
 +-- Argo CD
```

---

# 6. STEP 3 — VPC

`terraform/main.tf` mein AWS VPC module use hua hai.

Important:

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "~> 5.0"
}
```

VPC:

```text
10.0.0.0/16
```

create hota hai.

Uske andar:

```text
VPC
│
├── Public Subnets
│
└── Private Subnets
```

### Public subnet

Public subnet normally internet-facing components ke liye:

```text
Internet
   |
   v
Load Balancer
```

### Private subnet

EKS workloads private subnet mein run hote hain:

```text
EKS Nodes
   |
   +-- UI
   +-- Catalog
   +-- Cart
   +-- Checkout
   +-- Orders
```

Ye production architecture ke liye better design hai.

---

# 7. STEP 4 — NAT Gateway

Terraform mein:

```hcl
enable_nat_gateway = true
single_nat_gateway = var.enable_single_nat_gateway
```

Default:

```text
single_nat_gateway = true
```

Iska purpose:

Private subnet ke resources ko outbound internet access dena.

Example:

```text
Private EKS Node
      |
      v
NAT Gateway
      |
      v
Internet
```

Jaise Docker image pull karna, package download karna etc.

### Interview point

Aap bol sakte ho:

> "We use NAT Gateway to provide outbound internet connectivity to resources deployed in private subnets without exposing those resources directly to the internet."

---

# 8. STEP 5 — EKS Cluster

Terraform mein:

```hcl
module "retail_app_eks" {
  source  = "terraform-aws-modules/eks/aws"
}
```

Cluster:

```text
EKS
 |
 +-- Control Plane
 |
 +-- Compute
      |
      +-- General Purpose Node Pool
```

Project mein **EKS Auto Mode** enabled hai:

```hcl
cluster_compute_config = {
  enabled    = true
  node_pools = ["general-purpose"]
}
```

Ye important modern AWS EKS feature hai.

---

# 9. EKS networking

EKS:

```text
VPC
 |
 +-- Private Subnet AZ-1
 |
 +-- Private Subnet AZ-2
 |
 +-- Private Subnet AZ-3
```

EKS workloads private subnets mein run karte hain.

External user:

```text
Internet
   |
   v
AWS NLB
   |
   v
NGINX Ingress Controller
   |
   v
Kubernetes Services
```

---

# 10. STEP 6 — NGINX Ingress Controller

Terraform `addons.tf` mein:

```hcl
enable_ingress_nginx = true
```

Aur service:

```text
LoadBalancer
```

AWS NLB configure kiya gaya hai.

Flow:

```text
User Browser
     |
     v
Internet
     |
     v
AWS Network Load Balancer
     |
     v
NGINX Ingress Controller
     |
     v
UI Service
```

NGINX routing karta hai.

---

# 11. STEP 7 — SSL / Cert Manager

Project mein:

```hcl
enable_cert_manager = true
```

Cert-manager ka purpose:

```text
Let's Encrypt
     |
     v
TLS Certificate
     |
     v
Kubernetes Secret
     |
     v
NGINX Ingress
```

UI Helm values mein:

```yaml
cert-manager.io/cluster-issuer: "letsencrypt-prod"
```

Aur:

```yaml
tls:
  - secretName: tls-secret
```

So HTTPS architecture:

```text
Browser
   |
 HTTPS :443
   |
   v
AWS NLB
   |
   v
NGINX
   |
 TLS
   |
   v
UI
```

---

# 12. STEP 8 — Docker

Har microservice ka separate Dockerfile hai.

Example:

```text
src/
├── ui/Dockerfile
├── catalog/Dockerfile
├── cart/Dockerfile
├── checkout/Dockerfile
└── orders/Dockerfile
```

Ye **multi-stage Docker build** approach use karte hain.

---

# 13. UI Docker build

UI Java/Spring Boot application hai.

Build stage:

```text
Amazon Linux
   |
   +-- Maven
   +-- Java 21
   |
   v
mvn package
   |
   v
ui.jar
```

Final stage:

```text
Amazon Linux
   |
   +-- Java 21 runtime
   |
   v
app.jar
```

Important benefit:

```text
Build dependencies
       ❌
       |
       v
Final image
only runtime
```

Isse image relatively cleaner/smaller/security-friendly hoti hai.

---

# 14. Catalog service

Catalog different technology use karta hai:

```text
Go
+
Gin
+
GORM
+
MySQL
```

Docker:

```text
Go source
   |
   v
go build
   |
   v
main binary
   |
   v
Amazon Linux runtime
```

Catalog architecture:

```text
UI
 |
 v
Catalog Service
 |
 v
MySQL
```

---

# 15. Cart service

Cart:

```text
Java
Spring Boot
```

Database:

```text
DynamoDB
```

Flow:

```text
UI
 |
 v
Cart Service
 |
 v
DynamoDB
```

Helm values mein:

```yaml
dynamodb:
  create: false
```

Interesting point: application DynamoDB use kar sakti hai, lekin chart default mein local DynamoDB deployment create nahi karta.

---

# 16. Checkout service

Checkout:

```text
Node.js
+
NestJS
+
Redis
```

Flow:

```text
UI
 |
 v
Checkout
 |
 v
Redis
```

Aur checkout orders service ko call karta hai:

```yaml
orders: http://retail-store-orders:80
```

---

# 17. Orders service

Orders comparatively advanced service hai.

Technology:

```text
Java
Spring Boot
PostgreSQL
RabbitMQ
AWS SQS
```

Dependencies mein:

```text
spring-data-jdbc
PostgreSQL
Flyway
RabbitMQ
AWS SQS
OpenTelemetry
```

Architecture:

```text
Checkout
    |
    v
Orders Service
    |
    +------> PostgreSQL
    |
    +------> RabbitMQ
    |
    +------> AWS SQS
```

Interview mein ye service specifically explain kar sakte ho.

---

# 18. Kubernetes layer

Har service ka separate Helm chart hai:

```text
src/
│
├── ui/chart
├── catalog/chart
├── cart/chart
├── checkout/chart
└── orders/chart
```

Each chart generally create karta hai:

```text
Deployment
Service
ConfigMap
ServiceAccount
HPA
PDB
```

Depending on service:

```text
MySQL
Redis
RabbitMQ
PostgreSQL
DynamoDB
```

bhi create ho sakte hain.

---

# 19. Helm ka role

Suppose UI deployment hai.

Values:

```yaml
replicaCount: 1

image:
  repository: public.ecr.aws/aws-containers/retail-store-sample-ui
  tag: "1.2.2"
```

Helm template:

```text
values.yaml
     |
     v
deployment.yaml
     |
     v
Kubernetes Deployment
```

Iska benefit:

Same chart ko different environments mein use kar sakte ho:

```text
dev
staging
production
```

sirf values change karke.

---

# 20. Kubernetes Services

Microservices internally Kubernetes DNS use karte hain.

For example:

```yaml
catalog: http://catalog:80
carts: http://carts:80
checkout: http://checkout:80
orders: http://orders:80
```

Kubernetes DNS:

```text
catalog
carts
checkout
orders
```

resolve karta hai.

So UI ko pod IP pata hone ki zarurat nahi.

---

# 21. Internal communication

Example user product browse karta hai:

```text
Browser
   |
   v
NLB
   |
   v
NGINX
   |
   v
UI
   |
   v
Catalog Service
   |
   v
MySQL
```

Add-to-cart:

```text
UI
 |
 v
Cart
 |
 v
DynamoDB
```

Checkout:

```text
UI
 |
 v
Checkout
 |
 +----> Redis
 |
 v
Orders
 |
 +----> PostgreSQL
 |
 +----> RabbitMQ
```

---

# 22. Argo CD

Ab DevOps ka most important part.

Terraform Argo CD install karta hai:

```text
terraform/argocd.tf
```

Argo CD:

```text
Git Repository
      |
      v
   Argo CD
      |
      v
 Kubernetes
```

Ye **GitOps** hai.

Meaning:

> Git repository becomes the source of truth for Kubernetes deployment configuration.

---

# 23. Argo CD Application

Example:

```yaml
kind: Application
metadata:
  name: retail-store-ui
```

Argo CD ko bataya gaya:

```text
Repository:
GitHub

Branch:
main

Path:
src/ui/chart
```

Then:

```text
GitHub
   |
   | Helm Chart
   v
Argo CD
   |
   v
Kubernetes
   |
   v
UI Deployment
```

---

# 24. Argo CD Auto Sync

Configuration:

```yaml
syncPolicy:
  automated:
    prune: true
    selfHeal: true
```

### selfHeal

Agar kisi ne manually Kubernetes resource change kar diya:

```text
Git = desired state
K8s = changed state
```

Argo CD detect karega:

```text
Drift detected
      |
      v
Restore Git state
```

### prune

Git se resource remove ho gaya:

```text
Git resource deleted
       |
       v
Argo CD
       |
       v
Kubernetes resource deleted
```

---

# 25. GitOps Production flow

Ye interview mein **exactly** aise explain karna:

```text
Developer
    |
    | git push
    v
GitHub - gitops branch
    |
    v
GitHub Actions
    |
    +--> Detect changed service
    |
    +--> Docker build
    |
    +--> Security/Test
    |
    +--> Push image to ECR
    |
    +--> Update Helm image tag
    |
    v
Git commit
    |
    v
Argo CD detects Git change
    |
    v
Helm rendering
    |
    v
Kubernetes
    |
    v
New Pod
    |
    v
New Application Version
```

---

# 26. ECR

Production architecture mein:

```text
GitHub Actions
       |
       v
Docker Build
       |
       v
Amazon ECR
```

Example:

```text
123456789.dkr.ecr.region.amazonaws.com/
        |
        +-- retail-store-ui
        +-- retail-store-catalog
        +-- retail-store-cart
        +-- retail-store-checkout
        +-- retail-store-orders
```

Image tag:

```text
commit hash
```

Example:

```text
retail-store-ui:a82f91c
```

Iska benefit:

Har deployment traceable hai.

```text
a82f91c
   |
   v
Git commit
   |
   v
Exact application version
```

---

# 27. Public vs Production branch

Project mein interesting branching strategy hai.

### Main

```text
main
 |
 +-- Public ECR
 +-- Stable images
 +-- Manual deployment
```

### GitOps

```text
gitops
 |
 +-- Private ECR
 +-- GitHub Actions
 +-- Automatic image update
 +-- Argo CD
```

Comparison:

| Feature          | Main           | GitOps      |
| ---------------- | -------------- | ----------- |
| Image            | Public ECR     | Private ECR |
| CI/CD            | Limited/manual | Automated   |
| Deployment       | Manual/Argo    | GitOps      |
| Image tag        | 1.2.2          | Commit hash |
| Target           | Learning/demo  | Production  |
| Change detection | Manual         | Automatic   |

---

# 28. Important issue I found in the ZIP

Ek important inconsistency hai jo aapko **real project mein deploy karne se pehle understand karna chahiye**.

`README.md` ke according main branch:

```text
Umbrella chart
retail-store-app
```

use karna chahiye.

Lekin ZIP mein actual Argo CD files:

```text
retail-store-ui.yaml
retail-store-cart.yaml
retail-store-catalog.yaml
retail-store-checkout.yaml
retail-store-orders.yaml
```

hain, aur ye individual charts point kar rahe hain.

For example:

```text
src/ui/chart
src/cart/chart
...
```

So repository documentation aur actual current YAML configuration mein **difference** hai.

Interview ke liye iska concept samajhna important hai, lekin deployment karte waqt actual branch/version ko verify karna hoga.

---

# 29. Umbrella Helm chart kya hai?

`src/app/chart/Chart.yaml` mein:

```text
cart
catalog
checkout
orders
ui
```

sab dependencies hain.

Architecture:

```text
retail-store-sample-chart
        |
        +-- cart chart
        +-- catalog chart
        +-- checkout chart
        +-- orders chart
        +-- ui chart
```

Isko **umbrella chart** kehte hain.

Benefit:

```text
helm install retail-store-sample-chart
```

se complete application deploy ki ja sakti hai.

---

# 30. Monitoring capability

Project mein monitoring ke hooks already hain.

For example:

```yaml
metrics:
  enabled: true
```

Aur:

```yaml
prometheus.io/scrape: "true"
```

OpenTelemetry bhi project mein present hai:

```text
OpenTelemetry
```

UI/Java:

```text
Micrometer
Prometheus
OpenTelemetry
```

Catalog:

```text
OpenTelemetry
Prometheus
```

Checkout:

```text
OpenTelemetry
Prometheus
```

Orders:

```text
OpenTelemetry
Prometheus
```

Terraform mein monitoring stack currently disabled hai:

```hcl
enable_monitoring = false
```

So project **monitoring-ready** hai, but Prometheus/Grafana automatically enabled nahi hain in current Terraform configuration.

---

# 31. Security

Kubernetes security bhi reasonably achhi hai.

For example:

```yaml
runAsNonRoot: true
```

and:

```yaml
readOnlyRootFilesystem: true
```

and:

```yaml
capabilities:
  drop:
    - ALL
```

Meaning containers ko unnecessarily root privileges nahi diye gaye.

Docker image mein bhi:

```text
appuser
UID 1000
```

use kiya gaya hai.

Interview mein ye strong point hai.

---

# 32. HPA

Charts mein HPA configuration present hai:

```yaml
autoscaling:
  enabled: false
  minReplicas: 1
  maxReplicas: 10
```

Current default:

```text
HPA = disabled
```

But production mein enable kar sakte ho:

```text
CPU 50/80%
       |
       v
HPA
       |
       v
Pods increase
```

Example:

```text
1 pod
 ↓
High CPU
 ↓
HPA
 ↓
3 pods
```

---

# 33. PDB

PodDisruptionBudget bhi charts mein present hai:

```yaml
podDisruptionBudget:
  enabled: false
```

Purpose:

```text
Node maintenance
      |
      v
Kubernetes eviction
      |
      v
Ensure minimum pods remain available
```

---

# 34. Complete end-to-end request flow

Ab ek real user request samajho.

User browser mein:

```text
https://retail-store....
```

open karta hai.

### Step 1

```text
Browser
```

### Step 2

DNS:

```text
Domain
   |
   v
AWS Load Balancer
```

### Step 3

AWS NLB:

```text
NLB
 |
 v
NGINX Ingress Controller
```

### Step 4

NGINX:

```text
Ingress
 |
 v
UI Service
```

### Step 5

UI Pod:

```text
UI
 |
 +----> Catalog
 |
 +----> Cart
 |
 +----> Checkout
 |
 +----> Orders
```

### Step 6

Catalog:

```text
Catalog
   |
   v
MySQL
```

Cart:

```text
Cart
 |
 v
DynamoDB
```

Checkout:

```text
Checkout
 |
 +--> Redis
 |
 +--> Orders
```

Orders:

```text
Orders
 |
 +--> PostgreSQL
 |
 +--> RabbitMQ
```

---

# 35. Infrastructure deployment order

Aapko actual project ko deploy karna ho to conceptual order:

```text
1. AWS credentials
       ↓
2. Terraform init
       ↓
3. Terraform plan
       ↓
4. Terraform apply
       ↓
5. VPC
       ↓
6. EKS
       ↓
7. EKS addons
       ↓
8. NGINX
       ↓
9. Cert Manager
       ↓
10. Argo CD
       ↓
11. kubeconfig
       ↓
12. Argo CD Applications
       ↓
13. Helm
       ↓
14. Kubernetes Deployments
       ↓
15. Services
       ↓
16. NLB
       ↓
17. Application accessible
```

---

# 36. Actual commands ka flow

AWS configure:

```bash
aws configure
```

Terraform:

```bash
cd terraform

terraform init

terraform validate

terraform plan

terraform apply
```

Kubeconfig:

```bash
aws eks update-kubeconfig \
  --region us-west-2 \
  --name retail-store
```

Check cluster:

```bash
kubectl get nodes
```

Check all pods:

```bash
kubectl get pods -A
```

Check Argo:

```bash
kubectl get pods -n argocd
```

Check applications:

```bash
kubectl get applications -n argocd
```

Check retail:

```bash
kubectl get pods -n retail-store
```

Check services:

```bash
kubectl get svc -n retail-store
```

Check ingress:

```bash
kubectl get ingress -A
```

NLB:

```bash
kubectl get svc -n ingress-nginx
```

---

# 37. Argo CD login

Project Terraform Argo CD ko install karta hai.

Password:

```bash
kubectl -n argocd get secret \
argocd-initial-admin-secret \
-o jsonpath='{.data.password}' | base64 -d
```

Port forwarding:

```bash
kubectl port-forward \
svc/argocd-server \
-n argocd \
8080:443
```

Then:

```text
https://localhost:8080
```

---

# 38. DevOps interview mein aapka project explanation

Aap interview mein **code-by-code explain mat karna**.

Ye sequence follow karna:

### 1. Project introduction

> "This is an AWS EKS based microservices retail application. The application consists of five services: UI, Catalog, Cart, Checkout and Orders. We containerize each service using Docker and deploy them on Amazon EKS using Helm. Infrastructure is provisioned using Terraform and application deployment is managed using Argo CD following GitOps principles."

### 2. Infrastructure

```text
Terraform
 ↓
VPC
 ↓
Private/Public Subnets
 ↓
NAT Gateway
 ↓
EKS
```

### 3. Containerization

```text
Application
 ↓
Docker
 ↓
ECR
```

### 4. Kubernetes

```text
EKS
 ↓
Helm
 ↓
Deployment
 ↓
Service
```

### 5. Networking

```text
Internet
 ↓
NLB
 ↓
NGINX Ingress
 ↓
UI
```

### 6. Microservices

```text
UI
 ├── Catalog → MySQL
 ├── Cart → DynamoDB
 ├── Checkout → Redis
 └── Orders → PostgreSQL/RabbitMQ
```

### 7. GitOps

```text
GitHub
 ↓
GitHub Actions
 ↓
ECR
 ↓
Helm values
 ↓
Argo CD
 ↓
EKS
```

---

# 39. Interview mein "What happens when developer pushes code?"

Ye question almost certainly aa sakta hai.

Best answer:

> "When a developer pushes code to the GitOps branch, GitHub Actions detects which microservice has changed. It builds the corresponding Docker image, runs the required build and validation steps, and pushes the image to a private Amazon ECR repository using the commit hash as the image tag. The workflow then updates the Helm chart with the new image tag and commits the configuration change back to Git. Argo CD continuously monitors the Git repository, detects the desired-state change, synchronizes the Helm chart with the EKS cluster and Kubernetes performs a rolling deployment of the updated service."

Ye **strong DevOps answer** hai.

---

# 40. Is project mein technologies ka role

| Technology     | Role                    |
| -------------- | ----------------------- |
| Git/GitHub     | Source code             |
| GitHub Actions | CI/CD                   |
| Docker         | Containerization        |
| ECR            | Container registry      |
| Terraform      | AWS infrastructure      |
| AWS VPC        | Network                 |
| AWS EKS        | Kubernetes              |
| Helm           | Kubernetes packaging    |
| Argo CD        | GitOps/CD               |
| NGINX Ingress  | Traffic routing         |
| AWS NLB        | External load balancing |
| Cert Manager   | SSL certificates        |
| Let's Encrypt  | TLS certificates        |
| MySQL          | Catalog DB              |
| DynamoDB       | Cart DB                 |
| Redis          | Checkout cache/data     |
| PostgreSQL     | Orders DB               |
| RabbitMQ       | Messaging               |
| Prometheus     | Metrics                 |
| OpenTelemetry  | Observability/tracing   |
| Kubernetes HPA | Autoscaling             |
| PDB            | Availability            |

---

## 41. Aapke liye sabse important learning path

Aap is ZIP ko **ek saath 700 files** ki tarah mat padho.

Is order mein samjho:

```text
PHASE 1
AWS Architecture
   ↓
VPC
   ↓
Subnets
   ↓
NAT
   ↓
EKS

PHASE 2
Docker
   ↓
5 Dockerfiles
   ↓
ECR

PHASE 3
Kubernetes
   ↓
Deployment
   ↓
Service
   ↓
ConfigMap
   ↓
Secret
   ↓
Ingress
   ↓
HPA
   ↓
PDB

PHASE 4
Helm
   ↓
values.yaml
   ↓
templates
   ↓
umbrella chart

PHASE 5
Argo CD
   ↓
Application
   ↓
Sync
   ↓
Self Heal
   ↓
Prune

PHASE 6
GitHub Actions
   ↓
Build
   ↓
ECR
   ↓
Helm update

PHASE 7
Monitoring
   ↓
Prometheus
   ↓
OpenTelemetry
   ↓
Grafana
```

### Bottom line

**Ye ek achha end-to-end DevOps interview project hai.** Isme sirf Kubernetes deployment nahi hai; aap **Terraform → AWS VPC → EKS → Docker → ECR → Helm → Argo CD → GitOps → NGINX → SSL → Microservices → Databases → Monitoring** complete story bana sakte ho.

Aapke **EKS/DevOps interview preparation** ke liye main next step mein is ZIP ko **file-by-file nahi, balki actual implementation order mein** tod sakta hoon: **`Terraform → EKS → Docker → Helm → ArgoCD → GitHub Actions → complete deployment`**, aur har step ke saath **"ye file kya karti hai + interview mein kya bolna hai + commands + architecture"** explain kar sakta hoon.

=======================================

Yes. Based on the **above retail-store/EKS project architecture**, you can present it as a **realistic Fund Administration project** using your actual environment story, while replacing GitHub with **GitLab** and keeping the GitOps approach with **Argo CD**.

For interview, don't explain every technical file. Tell the story in this order:

## Fund Administration – DevOps Project Explanation

1. **Project Introduction**
   I am working with **UBS** in the Fund Administration domain. We manage multiple applications that support different stages of investment and fund-management activities.

2. **Business Requirement**
   The business works with multiple investment/start-up companies. The applications help manage activities such as fund calculations, client communication, reporting, UI operations and other backend processing.

3. **Application Landscape**
   We have **20+ applications**, and these applications are developed using different technologies such as **Java, .NET, Node.js and other technologies**.

4. **My Responsibility**
   My responsibility is mainly around **DevOps, environment management, infrastructure provisioning and application deployments** across different environments.

5. **Source Code Management**
   We use **GitLab** for source-code management. Developers push their application code to GitLab repositories.

6. **CI/CD Pipeline**
   Whenever developers commit code, the CI/CD pipeline gets triggered. The pipeline performs activities such as **build, unit testing, code quality checks, security scanning and container image creation**.

7. **SonarQube**
   We use **SonarQube** for static code analysis. It helps identify code-quality issues, bugs, code smells and security-related issues before deployment.

8. **Trivy**
   We use **Trivy** for vulnerability scanning of Docker images and dependencies. Before pushing an image to the registry, we check the image for known CVEs and vulnerabilities.

9. **Docker**
   We containerize the applications using **Docker**. Since we have applications developed in different languages, containerization provides a consistent runtime environment across different environments.

10. **Amazon ECR**
    After successful validation and security scanning, Docker images are pushed to **Amazon ECR**, which we use as our container image registry.

11. **Infrastructure Provisioning**
    We use **Terraform** to provision and manage AWS infrastructure. This includes components such as **VPC, subnets, security configuration and Amazon EKS**.

12. **Amazon EKS**
    Our containerized applications are deployed on **Amazon EKS**, which provides the Kubernetes platform for running and managing our microservices.

13. **Helm**
    We use **Helm charts** to package and deploy Kubernetes applications. Each application has its own deployment configuration, service configuration, resource settings and environment-specific values.

14. **GitOps Approach**
    We follow a **GitOps-based deployment model**. The desired Kubernetes configuration is maintained in GitLab, and **Argo CD** continuously monitors the repository.

15. **Argo CD**
    When there is a change in the deployment configuration, Argo CD detects the change and synchronizes the desired state with the EKS cluster. This gives us a controlled and auditable deployment process.

16. **Application Networking**
    For external access, we use **NGINX Ingress** with an AWS load balancer. Traffic comes from the client, reaches the load balancer and is routed through the ingress to the appropriate application service.

17. **Microservices Communication**
    Different applications communicate with each other through Kubernetes services. Depending on the application requirement, we use databases and supporting services such as **MySQL, PostgreSQL, Redis, DynamoDB and RabbitMQ**.

18. **Security & Reliability**
    We follow security practices such as container vulnerability scanning, SonarQube quality gates, non-root containers, Kubernetes resource controls and controlled access to AWS and EKS.

19. **Monitoring & Troubleshooting**
    We can integrate **Prometheus/OpenTelemetry and Grafana** for application and infrastructure monitoring. For issues, I troubleshoot across the complete stack—from GitLab pipeline and Docker image to ECR, Kubernetes pods, services, ingress and application logs.

20. **Overall DevOps Flow**
    Overall, the flow is:

```text
Developer
    ↓
GitLab
    ↓
CI/CD Pipeline
    ↓
Build & Test
    ↓
SonarQube
    ↓
Trivy Security Scan
    ↓
Docker Build
    ↓
Amazon ECR
    ↓
GitLab Deployment Configuration
    ↓
Argo CD
    ↓
Helm
    ↓
Amazon EKS
    ↓
NGINX Ingress / Load Balancer
    ↓
20+ Applications / Microservices
```

### ⭐ Short interview introduction

You can start your interview answer like this:

> **"Currently, I am working with UBS in the Fund Administration domain. We manage more than 20 applications developed using different technologies such as Java, .NET and Node.js. These applications support different business functions including UI, calculations, client communication, backend processing and reporting. My role is mainly focused on DevOps, environment management, infrastructure provisioning and application deployment. We use GitLab for source-code management, Terraform for AWS infrastructure, Docker for containerization, ECR for image management and Amazon EKS for Kubernetes-based deployments. For CI/CD, we use SonarQube for code-quality analysis and Trivy for vulnerability scanning. We follow a GitOps approach using Helm and Argo CD, where deployment configurations are maintained in GitLab and Argo CD synchronizes them with the EKS cluster. For application access, we use NGINX Ingress and AWS load balancing. So, I am involved in the complete flow from source-code commit to application deployment and troubleshooting in the EKS environment."**

This is a **good 2–3 minute project introduction**. Then, if the interviewer asks deeper questions, you can go into **Terraform → EKS → Docker → GitLab CI → Trivy → SonarQube → ECR → Helm → Argo CD → Kubernetes → NGINX** one by one.
