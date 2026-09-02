---
title: 1. DevOps
has_children: true
nav_order: 2
---

- [1. Linux ⭐ CORE](#Linux)
- [2. Git](#Git)
- [3. GitHub](#GitHub)
- [4. GitHub Actions](#GitHub-Actions)
- [5. GitLab CI/CD ⭐ CORE](#GitLab-CICD)
- [6. Jenkins ⭐ CORE](#Jenkins)
- [7. Docker](#Docker)
- [8. Kubernetes ⭐ CORE](#Kubernetes)
- [9. Helm ⭐ CORE](#Helm)
- [10. Argo CD](#Argo-CD)
- [11. Terraform ⭐ CORE](#Terraform)
- [12. AWS ⭐ CORE](#AWS)
- [13. Microsoft Azure ⭐ CORE](#Microsoft-Azure)
- [14. AWS vs Azure](#AWS-vs-Azure)
- [15. Ansible ⭐ CORE](#Ansible)
- [16. Bash / Shell Scripting ⭐ CORE](#Bash--Shell-Scripting)
- [17. Python](#Python)
- [18. YAML](#YAML)
- [19. JSON](#JSON)
- [20. Apache HTTP Server](#Apache-HTTP-Server)
- [21. Nginx](#Nginx)
- [22. Tomcat](#Tomcat)
- [23. JBoss-WildFly](#JBoss)
- [24. SSL/TLS](#SSLTLS)
- [25. Prometheus/Grafana/OpenTelemetry](#Prometheus)
- [26. LGTM Stack ⭐ CORE](#LGTM-Stack)
- [27. Splunk](#Splunk)
- [28. BigPanda](#BigPanda)
- [29. AI & Development Tools](#AI--Development-Tools)

---


# 🚀 DevOps Quick Review

<a id="Linux"></a>

## 1. Linux

### Core Linux Concepts

- Linux architecture
- Kernel
- Shell
- Filesystem hierarchy
- `/etc`, `/var`, `/home`, `/tmp`, `/opt`, `/usr`
- File types
- Absolute vs relative paths
- Environment variables
- `PATH`

### Essential Commands

```bash
pwd, ls, cd, cp, mv, rm, mkdir, touch, cat

less, head, tail, grep, find, locate, sort, uniq

cut, awk, sed, xargs, wc, tr

```

### Permissions

```bash
chmod, chown, chgrp, umask.
```

- Read / Write / Execute
- User / Group / Others
- Numeric permissions
- SUID
- SGID
- Sticky bit

### Users & Groups

```bash
useradd, usermod, userdel, groupadd, groupmod, groupdel

passwd, id, who, whoami, sudo, su
```

### Process Management

```bash
ps, top, htop, kill, pkill, jobs, bg, fg, nohup
```

### Services

```bash
systemctl
service
journalctl
```

### Disk & Memory

```bash
df
du
free
lsblk
mount
```

### Networking

```bash
ping, curl, wget, ss, netstat
nslookup, dig, traceroute
ip, hostname
```

### SSH

```bash
ssh
scp
sftp
ssh-keygen
```

### Logs

- `/var/log`
- Application logs
- System logs
- `journalctl`
- `tail -f`

### Linux Troubleshooting Scenarios

```text
High CPU
High Memory
Disk Full
Process Down
Service Down
Port Not Accessible
Permission Denied
Application Not Responding
Network Connectivity Issue
Log Analysis
```

---

<a id="Git"></a>

# 2. Git

## Git Fundamentals

```text
Working Directory
       ↓
   git add
       ↓
Staging Area
       ↓
 git commit
       ↓
Local Repository
       ↓
  git push
       ↓
Remote Repository
```

### Essential Commands

```bash
git init, git clone, git status, git add, git commit
git push, git pull, git fetch
git log, git diff
git branch, git switch, git checkout, git merge
git rebase, git stash, git reset, git revert, git tag
```

### Git Concepts

- Repository
- Working Directory
- Staging Area
- Commit
- Branch
- HEAD
- Remote
- Origin
- Merge
- Rebase
- Conflict
- Tag
- `.gitignore`

### Git Troubleshooting

- Merge conflicts
- Rebase conflicts
- Undo commit
- Undo changes
- Recover deleted branch
- `reset` vs `revert`
- `merge` vs `rebase`

---

=================================

<a id="GitHub"></a>

# 3. GitHub

## GitHub Repository

- Repository
- Public vs Private
- README
- `.gitignore`
- Branches
- Tags
- Releases
- Repository Settings

## GitHub Branches

```text
main
 │
 ├── develop
 │
 ├── feature/login
 │
 └── bugfix/payment
```

## Pull Request

```text
Developer
   ↓
Feature Branch
   ↓
Push
   ↓
Pull Request
   ↓
Code Review
   ↓
CI Checks
   ↓
Approval
   ↓
Merge
```

### GitHub Features

- Issues
- Pull Requests
- Projects
- Wiki
- Releases
- Actions
- Environments
- Packages
- Security

### GitHub Security

- Personal Access Token
- SSH Keys
- Repository Secrets
- Variables
- Branch Protection
- CODEOWNERS
- Dependabot
- Secret Scanning

=================================

---

<a id="GitHub-Actions"></a>

# 4. GitHub Actions

### Core Concepts

```text
Workflow
   ↓
Job
   ↓
Steps
   ↓
Actions
   ↓
Runner
```

### Important Concepts

- Workflow
- Trigger
- Event
- Job
- Step
- Runner
- Action
- Environment
- Variables
- Secrets
- Artifacts
- Matrix Strategy
- Dependencies
- Manual Workflow

### Basic Workflow

```yaml
name: CI

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Build
        run: echo "Build application"
```

---

===========================================

<a id="GitLab-CICD"></a>

# 5. GitLab CI/CD

### Architecture

```text
.gitlab-ci.yml
      ↓
   Pipeline
      ↓
    Stages
      ↓
     Jobs
      ↓
    Runner
```

### Important Concepts

- `.gitlab-ci.yml`
- Pipeline
- Stage
- Job
- Runner
- Variables
- Secrets
- Artifacts
- Cache
- Environment
- Rules
- `needs`
- Manual Jobs
- Dependencies

### Basic Structure

```yaml
stages:
  - build
  - test
  - deploy

build:
  stage: build

test:
  stage: test

deploy:
  stage: deploy
```

---

====================================

<a id="Jenkins"></a>

# 6. Jenkins

![Image](https://images.openai.com/static-rsc-4/q62ISvFLB27PmTb0mnyKiHMwxOqWh-mdhSgQwmP9r97YJ08GkMdIqcc5Paw2or23PWPwpHhEhHf9CngperW-icxUJ3Bl5QRlGZHGDbY9r8VO0j-BOHCO710RR15QqABksU8iPjj8eaemuIpQJambcgobxd6BoeVd6jG3Bh73i1bWqsW4u4w0anFAER328pdP?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/M0McNmp6Ar2k1q5n8GNk5hNpojKmSvLRb7TwrJhGalRx_iNY89ToRKj1foLrlHAHBwmuyyaG80TXNgKo3wc_SZyyKQ04zGIaegQW9WcF1LGfp85nm_TsJxlCzdYiNoPJFdgFacm1n8TqPSOz3DZmj5VZBGJFTpwqf48QZCDkEgW8HAKw3CJ06ITsLXMs6vPD?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/riRWsGXECh6nSs8PNMBtAVsdL-00Befn6VMkYoSIPTzE3PevgiVaGleB6useGrZvdieZscAl0I9mbEcHnuDdcyGLNM_KdgkxTicw8RIcniRU2t1OeS6vDWNVgJ4LD9FnUTldKp836tae1DkbxPxeXlG3ZBvMoCdmNX3fYOaODApghPPdGViYCRA9xBk8SBdb?purpose=fullsize)

## Jenkins Architecture

```text
Developer
    ↓
GitHub / GitLab
    ↓
Jenkins
    ↓
Build
    ↓
Test
    ↓
Docker Build
    ↓
Container Registry
    ↓
Kubernetes
```

### Important Concepts

- Controller
- Agent
- Job
- Pipeline
- Freestyle Project
- Jenkinsfile
- Stage
- Step
- Plugin
- Credentials
- Webhook
- Parameter
- Environment Variable
- Artifact

### Jenkins Pipeline

```groovy
pipeline {
    stages {

        stage('Build') {
            steps {
                echo 'Building'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
}
```

---

====================================

<a id="Docker"></a>

# 7. Docker

![Image](https://images.openai.com/static-rsc-4/MhqbBYC9SrDJU52tl_s35R-JXw_BrSvNMFIRiTJEWpDgkCYQFZNk3YDhXwcaKXFAA5xB3CMf7s6CgH7o3Mv4hmTBtSlZRZqq19HMJ84RQP21z9ucP4CHtYqChU_Jz1JVY7vtXvVkvLYdQxHqp4_9gfk5ddZzmv68TKzAjzA8ngwdNGN1cp_hlSQrbsCPb67F?purpose=fullsize)

## Docker Architecture

```text
Docker Client
     ↓
Docker Daemon
     ↓
Docker Images
     ↓
Docker Containers
```

### Core Concepts

- Image
- Container
- Dockerfile
- Docker Engine
- Docker Daemon
- Registry
- Docker Hub
- ECR
- ACR
- Volume
- Network
- Port Mapping
- Environment Variables
- Layers
- Multi-stage Build

### Commands

```bash
docker build
docker images
docker run
docker ps
docker exec
docker logs
docker stop
docker start
docker restart
docker rm
docker rmi
docker pull
docker push
docker inspect
docker network
docker volume
```

### Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

---

===============================

<a id="Kubernetes"></a>

# 8. Kubernetes

![Image](https://images.openai.com/static-rsc-4/4S3EOvEj8B_PzAOrMoa_Al6gkHrQagkOXtXIDB2-L_EDR1vOYrgfmB3w4ehSEHh7uI90_62xTeegx3dQP4x8yoxk2eIPm-c_BbBFQRVwkkcyuP_PkpDbnAWjTJcXah5VY1q42tfdMGcJFUa_0Zna-awUg-GyJqoPiWAQMfUDsUNLqIDYIhjyiBg-_N35GDTo?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/SdAbRM1sc7LyRFsMuPkLLV2ygIapYsDlryKimNaW1EpZ7ntR9MgDlUAbbd3qsblanP3P8YFomEXVa59Kr7hbiCvrp-XuZc-2Aw5WPXgMHwkn_7iMsuVuOKPh_cjvKJq48lPgnOZ4gPQk8DIYka7x5wy3sNXP9PWPqQ8oK8g03-M7vNHtLf8DkJL73P_2z_X0?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/N9gIqQrCIbdFDrqCD0Zr1jMrj2Wcq9dOuTi-Utr6UIT2Bpaj80IYm5xZb_aOfv73dBzxNUlzXeg9naNVyPiGOsmAHSu_fS8FbRq48VRZ1FbJB_hv7SJQK941qSfOKTd8WHwdHPQ6YYGcGQ4Ml7IdbkYkoaQ8HtEBkHavKx3vvEizWM55o3DMUZ7dITXiG0ug?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/B_LM1nMQKOpyKMKYeY872FxwFPM5BJNDIsDowuBa-hLyYkNd7edP72nOHA2wB8JuuYCHu8WV26z6iwDS2wPHLVpcXTNRzauWmND_KYBusnxby8Q2XKZzT9QL1rVzlgR93pWjS1USh57b95aC5ZCAI4ezrcEs3QYSR-8aPZtVk1Sp2aNSxsCfp9t3uKvK90uu?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/fgMw-MKJasQQwMRge-QPZaV7VgNXA7W3PlxLtzoT_752nrREy_9NudkCESGF3GdbA08C-s79gA_WAuSu5SyKQUBv10Mqqp2-YwhtGIFLZYBYF68Iy463BLHGlChrNKZMumvgLTFVI3-ABP6mFtfMjvNOgE2p_A9IYAgksLqZubvBfpxnDreH_jag7tH_6SQy?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/MKvq2377D0M1HSvFjSwK7U48Gkj3O3BYUGGUbagMjV3HGPpNo5NIJucsaLQWZzO5sRVPlAN1R2JE4WJVvd2_BcXa8UfAOWiEuQLI4uNROnRmwyajDtFXxSMb_kUVlxcb1fuImSmTQzBLxRObvbblqUGwU5VUsqQEkvCXmDryaHRrn4CD4zO98J7Sk-AZ1fZJ?purpose=fullsize)

## Kubernetes Architecture

### Control Plane

```text
                 Control Plane
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
  API Server      Scheduler     Controller
       │
      etcd
```

### Worker Node

```text
Worker Node
│
├── kubelet
├── kube-proxy
└── Container Runtime
        │
       Pods
        │
    Containers
```

### Control Plane Components

- API Server
- etcd
- Scheduler
- Controller Manager
- Cloud Controller Manager

### Worker Components

- kubelet
- kube-proxy
- Container Runtime

---

# 9. Kubernetes Resources

### Workloads

- Pod
- ReplicaSet
- Deployment
- StatefulSet
- DaemonSet
- Job
- CronJob

### Networking

- Service
- ClusterIP
- NodePort
- LoadBalancer
- Ingress
- Ingress Controller
- CoreDNS

### Configuration

- ConfigMap
- Secret

### Storage

- PersistentVolume
- PersistentVolumeClaim
- StorageClass

### Security

- ServiceAccount
- Role
- RoleBinding
- ClusterRole
- ClusterRoleBinding
- NetworkPolicy

### Scaling

- HPA
- VPA — basic

### Namespaces

- Namespace
- ResourceQuota
- LimitRange

---

# 10. Kubernetes YAML

### Basic Structure

```yaml
apiVersion:
kind:
metadata:
spec:
```

### Deployment Example

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx

spec:
  replicas: 3

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
```

### YAML Topics

- `apiVersion`
- `kind`
- `metadata`
- `spec`
- `metadata.name`
- `labels`
- `selector`
- `template`
- `containers`
- `image`
- `ports`
- `env`
- `resources`
- `volumeMounts`
- `volumes`
- `probes`

---

# 11. Kubernetes Networking

```text
Pod
 ↓
Service
 ↓
Ingress
 ↓
Load Balancer
 ↓
Internet
```

### Concepts

- Pod IP
- Service IP
- ClusterIP
- NodePort
- LoadBalancer
- Ingress
- Ingress Controller
- DNS
- CoreDNS
- Service Discovery
- NetworkPolicy

---

# 12. Kubernetes Storage

```text
Pod
 ↓
PVC
 ↓
PV
 ↓
StorageClass
 ↓
Cloud Storage
```

### AWS

- EBS
- EFS

### Azure

- Azure Disk
- Azure Files

---

=============================================

<a id="Helm"></a>

# 13. Helm

![Image](https://images.openai.com/static-rsc-4/YooEAd8EZHKkUfEgTUX7LFKEg03_kEqKW520Km1qaL48jkxJ-hNigEBUFJObliSGmv28n0_6JFhK45fEp7BB6HtNEBUGH6FZP9K5fnRtMK4nqom-VDpHBSGfhACRd_Qpe0t21hQ5GSkwE2PA9t8WkIrJBdqQl7Ftc3SSmhxiWmSFN68grzXgM5DnSkpPPGPO?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/_Q25cUkC6c_I5dhkKVxIII2XvZRkjxS9kALsGEbgYua6G3IJx6n-7CyFmbzpyVUtJtF0OVVruWHZOUfbo4PwMK5ecwkYqPFaAamF_MABtZC84A0ZMlZr7sXCaaBWxI9AjUoMSK7F8O1sHRqybUp1mWipYOm__nNr9qArS0aR-P1mlZu2PYrdpNXX4-UFNU8N?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/BN9WrSxwiRiIK_n4PJ0Q-xj_m_QllbQl17_pxaFWIbYcrohyDHOLUK7jRGGEDwgxk3OUBfufHa6LDv894xI2HI5Kd57VNFCuZmzjiGnGJouH470VbXRSMI5XQ3ljAHh5sCQDYqH-ofQByWnqFFfnpTaGg1yYaxFyroAJvBpFo2riK9vYZwJ6mtAzPIYzItW5?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/SBDFEJcf_sHjT2hKSEhdRm9Ad-EW73foHS5HXn4Cv0ROEVzba3sb0fwXlFqYOmyRZ1qr2HLI01QGwUnrh8Vok_4-isDUVj__bt7eoFRtX8NhxgfPWZvceK8QYaCSBE8ch3e7tZhLT1fzbIFXZO6C_-2kUHDQtK8gfxniaeIMihjAs5g9PZ3iILKfU9So1Sn0?purpose=fullsize)

## Helm Chart Structure

```text
Chart
├── Chart.yaml
├── values.yaml
└── templates/
      ├── deployment.yaml
      ├── service.yaml
      └── ingress.yaml
```

### Important Concepts

- Chart
- Release
- Repository
- `Chart.yaml`
- `values.yaml`
- Templates
- `_helpers.tpl`
- Template Functions
- Variables
- Conditions
- Loops

### Commands

```bash
helm repo add
helm repo update
helm search repo
helm install
helm upgrade
helm rollback
helm uninstall
helm list
helm history
helm template
helm lint
```

---

========================================

<a id="Argo-CD"></a>

# 14. Argo CD

![Image](https://images.openai.com/static-rsc-4/IOXp7AyfQj96NBaM4HP6U2Ngnlok5xTb8x6Yvqzqu5Q49bLcCIS0L18jLN2x_M-bH6JIwwlYm79cWPmEsJCjrjc31KCnChrrqV74VxljJIZ6eOZLnOiFzUQq2SNTEui4Yc80D5YTSRvR_r1A8oYhUKxLneTPn7lzFvLNwNoEJ4vhrO_bBARD5U4HL9BX33NF?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NBAIUsGyENh_jGHUIK_LcKkEoi9_tY4YZkOZ2ylJiSBqyig3tvcbcKLf5qqKjOOMPuJ-FayZhokeWjFqhu2j09h4zp8aNJBlcdl44uDMXY6KcYsCpfRU6_OQPHsNjxtq7RhGVBIzi3SgEqgnEAePcKxIEOdugnElw37bi230RX5fh3OCmL24yJ6fPQKxj2GU?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/OLpjz0UGO4iqdVu9QFnA-euRcmyZPjJBiVvWqly4ob0HQpwULzx_bMpKfLVh_tCmQxJ4JDHXbASIc733pholhjxx7henL3NLOe1UgEIbyAOSkUNPDYHpo83l3JMX1hQxMjaXkZuPX18ddo8SvLe3KeBRHrwD6prC2dxcGvoO6B-JlOKcZ0OGCEQR4QbdTSyv?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/lFGBziMK98BMclzkfpVzpwZlMZLsU9Ll8GgFYUMBy8vhqIDOuuEtgYf3-1NgLu4uWtTwNiDbNteiqBo77gHzIQTxBys79oee-u2GPi9qXfc78zfqtWKiJskuIB1uPXfMVoizemr8TQd_xNGGsyadZ09BckRm31zMYSWVA0bHra0CtnslvpdLQ87Rr2-vozDH?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/W0aJVrMWBMuM01WPcgaLfxtnbWKt57-Ma1WEOPXf__d-2KfS_KSbe8PceAdMIf2Uu7_FyGQQjEmbhLyC3LXlkkuWxAfGpIguGx_fvnR7SlhuecrJFIL87SVMs5M6aNFBdmYklN-4mF_bdhTgOwjELrQZUUPRQIDKBLDnDNUhZyie1g2nOfmJ9k0LMQMn02CN?purpose=fullsize)

## GitOps Flow

```text
Developer
    ↓
Git Repository
    ↓
Argo CD
    ↓
Kubernetes
```

### Important Concepts

- GitOps
- Desired State
- Actual State
- Synchronization
- Auto Sync
- Manual Sync
- Drift
- Application
- Project
- Repository
- ApplicationSet
- Health Status
- Sync Status

### CI vs CD

```text
Jenkins / GitHub Actions / GitLab
              ↓
             CI
       Build + Test + Image
              ↓
          Registry
              ↓
           Argo CD
              ↓
             CD
              ↓
         Kubernetes
```

---

=========================================

<a id="Terraform"></a>

# 15. Terraform

![Image](https://images.openai.com/static-rsc-4/KHZLGEw3rP4nZHho2eeCPd-EGF4hA3KYmdGlkAj5KvbjVouLuK35f7jF4-vTeVaI29kbkKlEbkvLv3Xn8RBYrbeXCO-tWJt_fjAruLAZ4kzKaC1yL4Y5cXaGwoXY8lPHLE5_khk3zaU0HTolZqoRz7jDqseVLtDLIZ2UmjUyjnpy0gCPXGgOSwAMkjO9l1m0?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/vy4SvdQ6sJKqptAW8ApFnaTweb2h3djO_uKTxusYM7z6At6mHegH3i_a0Tp2TNV5RoIQTuubbT5r9H7zkrUnSWvxkgWuorGvGRbl5XPVAARZd9Jgyr2ZU1UebwxLS1RmQyWl_U_srNlLSu5f6J59L0qQ7AslPq_PaIqrIBf4J6jiqpu0PnIALs0S_xs3tE7b?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/jP31BHTXIYpIwZhflr0O1LKBGmBFD8Gu1_6Hd3r1RJr6ln3pkrkHZvQiQ9bCCJR6atSoBgBjsKe5TdO6fS_nijCjStbccOYWszw6hyL9g-aI-fs1RFFK_lSm3_jQlaoL5MfL_S7hhnwmPX-wW_cgXkKuSgfBnIQa-S1tlhnL2_gX3fGy4OSVIzLAVMmYTK9D?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/aee1qjVGJvp5p6RWy0FpTIS9KaJkB3VdS9F4a-2uuLKO_tGX0SE523YZVtFfhFf3YIMrSvxLYltvyyBwn6QgUeD51AJd6dtBF8bq_mCLRHC65T8Z9sPHPvYfujDoRk-ujWZpSVUTuQkXbEAv-r1rDgN30GaN165p-09aL_Q6Vw4bEP8hZmPyp25QAiDg8G0Y?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/9A0GNE34tU5NUgLyQGq8JpxBbU6iN6yYWFWAP4AdZDJyWgvyRnhTtN6ptsCSkenNmohSQZzD7JvgEEAKv-9zZBDuM_a9lMZ_NFh3F8bVX-SMi21xbhBKYP3ZZKX16jFIU3CLVMA0nb5iHPlSITOc48d0TEtGiYV0B6UM1dvSNVA0TOLYgOQ-VtOvNLi2nwK9?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/i2_TPXtFPx_Is1Frdn9Lbb7ngAOgLpY-HgIh1OX7CwuoopVHP00x5I-gOG2qViaUsbpuXHs8JqVrPsWldbs7noGzwhHeycuRMQ44E3b_TjD8enBAxu601stCg4sLHjeFLJgbr4uK1YqvpR72QPLx_DxF8nICnv_P2C0ixM-zlkMM4hVMG2frpzs8oZ3NGgeZ?purpose=fullsize)

## Terraform Workflow

```text
Terraform Code
      ↓
terraform init
      ↓
terraform validate
      ↓
terraform plan
      ↓
terraform apply
      ↓
Cloud Infrastructure
```

### Important Concepts

- Provider
- Resource
- Variable
- Local
- Output
- Module
- State
- Backend
- Data Source
- Dependency
- Workspace
- Provisioner — basic

### Commands

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
terraform state
terraform import
terraform show
terraform output
```

---

====================================

<a id="AWS"></a>

# 16. AWS

## Compute

- EC2
- Auto Scaling
- Elastic Load Balancer
- ECS
- EKS
- Lambda

## Networking

```text
VPC
├── Public Subnet
│     └── Internet-facing Resources
│
└── Private Subnet
      └── Application / Database
```

Know:

- VPC
- Subnet
- Route Table
- Internet Gateway
- NAT Gateway
- Security Group
- NACL
- Route 53

## Storage

- S3
- EBS
- EFS

## Security

- IAM
- Users
- Groups
- Roles
- Policies
- Access Keys
- KMS
- Secrets Manager

## DevOps

- ECR
- EKS
- CodeBuild
- CodePipeline
- CloudWatch
- CloudFormation — basic

---

====================================

<a id="Microsoft-Azure"></a>

# 17. Microsoft Azure

## Core Services

- Subscription
- Resource Group
- Region
- Availability Zone
- Virtual Machine
- VNet
- Subnet
- NSG
- Load Balancer
- Application Gateway

## Storage

- Storage Account
- Blob Storage
- Azure Files
- Managed Disk

## Identity & Security

- Microsoft Entra ID
- Managed Identity
- RBAC
- Key Vault

## DevOps

- Azure DevOps
- Azure Repos
- Azure Pipelines
- Azure Artifacts
- Azure Boards
- Azure Container Registry
- AKS

---

====================================

<a id="AWS-vs-Azure"></a>

# 18. AWS vs Azure

| AWS             | Azure           |
| --------------- | --------------- |
| EC2             | Virtual Machine |
| VPC             | VNet            |
| Subnet          | Subnet          |
| IAM             | Entra ID + RBAC |
| S3              | Blob Storage    |
| EKS             | AKS             |
| ECR             | ACR             |
| CloudWatch      | Azure Monitor   |
| Secrets Manager | Key Vault       |
| Route 53        | Azure DNS       |
| Security Group  | NSG             |
| CloudFormation  | ARM/Bicep       |

---

====================================

<a id="Ansible"></a>

# 19. Ansible

## Architecture

```text
Control Node
      ↓
     SSH
      ↓
Managed Nodes
```

### Important Concepts

- Inventory
- Playbook
- Play
- Task
- Module
- Handler
- Variable
- Facts
- Roles
- Templates
- Idempotency
- Ansible Vault

### Example

```yaml
- hosts: webservers
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present

    - name: Start nginx
      service:
        name: nginx
        state: started
```

---

<a id="Bash--Shell-Scripting"></a>


# 20. Bash / Shell Scripting

### Core Concepts

```bash
#!/bin/bash

variables
if
else
elif
for
while
case
functions
```

### Special Variables

```bash
$1
$2
$?
$#
$@
$USER
$HOME
```

### Important Commands

```bash
grep
awk
sed
cut
sort
uniq
find
xargs
wc
tr
```

### Practice Scripts

- System Health Check
- User Creation
- Log File Analyzer
- Automatic Backup
- Disk Cleanup
- SSL Certificate Expiry Checker
- Service Check
- File Monitoring

---
<a id="Python"></a>


# 21. Python

### Core Python

- Variables
- Data Types
- Lists
- Tuples
- Sets
- Dictionaries
- Conditions
- Loops
- Functions
- Exception Handling
- File Handling

### DevOps Python

- `os`
- `sys`
- `subprocess`
- `json`
- `requests`
- YAML parsing
- REST APIs
- AWS automation
- Azure automation
- Log processing

---
<a id="YAML"></a>

# 22. YAML

Used in:

```text
Kubernetes
GitHub Actions
GitLab CI/CD
Ansible
Azure Pipelines
Helm
```

### Important Concepts

```yaml
key: value

list:
  - item1
  - item2

object:
  name: application
  environment: production
```

Know:

- Indentation
- Lists
- Objects
- Nested structures
- Strings
- Boolean
- Numbers
- Multiline values
- Variables
- Anchors

---
<a id="JSON"></a>

# 23. JSON

Example:

```json
{
  "name": "application",
  "environment": "production",
  "replicas": 3
}
```

### Concepts

- Object
- Array
- Key/Value
- String
- Number
- Boolean
- `null`

### Used With

- REST APIs
- AWS CLI
- Azure CLI
- Terraform
- Python
- Kubernetes

---
<a id="Apache-HTTP-Server"></a>

# 24. Apache HTTP Server

### Important Topics

- Web Server
- Virtual Host
- Reverse Proxy
- Load Balancing
- SSL/TLS
- HTTP → HTTPS
- Modules
- Configuration
- Access Logs
- Error Logs

---
<a id="Nginx"></a>

# 25. Nginx

### Important Topics

- Web Server
- Reverse Proxy
- Load Balancer
- Static Files
- SSL Termination
- HTTP → HTTPS
- Configuration
- Access Logs
- Error Logs

### Architecture

```text
Client
  ↓
Nginx
  ↓
Application
  ↓
Tomcat
  ↓
Database
```

---
<a id="Tomcat"></a>

# 26. Tomcat

### Important Topics

- Web Container
- WAR File
- Deployment
- `server.xml`
- `web.xml`
- `context.xml`
- Logs
- Ports
- JVM
- Heap
- Garbage Collection
- Service Management

---
<a id="JBoss"></a>

# 27. JBoss / WildFly


### Important Topics

- Application Server
- WAR
- EAR
- Deployment
- Datasource
- JVM
- Management Console
- CLI
- Logs
- Standalone Mode
- Domain Mode

---

<a id="SSLTLS"></a>
# 28. SSL/TLS

```text
HTTP
 ↓
HTTPS
 ↓
TLS
 ↓
Certificate
```

### Important Concepts

- SSL vs TLS
- Certificate
- Private Key
- Public Key
- CSR
- Certificate Authority
- Root CA
- Intermediate CA
- Certificate Chain
- PEM
- CRT
- KEY
- P12
- PFX
- HTTPS
- TLS Handshake
- Certificate Expiry
- Hostname Mismatch

### Commands

```bash
openssl s_client
openssl x509
curl -v
```

---

====================================

<a id="Prometheus"></a>

# 29. Prometheus

![Image](https://images.openai.com/static-rsc-4/gyzBfCmmRoeqnbZ9Cj12_0FfNGlhOzg-zuJDE92AlUHawIVk8Eq2VxKJChFF2CayRYPMzwBCR6B4Au6JMVu7YuqUyQv9TV2FgZsbB4J2tu_2rl3yWaW3uZut-gDjKJj3zWDPtON_daaqmL1c3fYVfL6dUdyYdGL0j94m5qgXWs4K13aJE9n_czvZMZ0-4CCa?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/p6nDYkCiH-bF_fTKJ8uqSMRgpUATHyzYi_dFp12l_BUy9YO8jIsGePPoRSUif7FxO_v8L3VXEiL2a1R_B5BCvB-3tO7VloLrx3X4EWRCoz0b8hHy_3nDJS0NkAFnkOToNIH_LNgfzMuytPfDSGfCxJ6t8PYRt1gV3YwSMl85dq-e0RIFgc4_kv5G20BTm0mj?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Mw62-qA58VE3yn-AKB-A0ZePIp9914mn1uPXcKGjUIrtGonDW5a556h_2BQ1n9baOj93u-KADPtMUBOmT4GRWzecqzHLMHb9sS4FN0-jS28YsAkTWTLRMXVoYOMdFQ7R-LvkNtWu5jgQu_NGjjYb40xuXex4JMyt5gCUBpJUKdQshkv8U60Jm8WCQbC7AmkW?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/MzAFFXnOL-Exm4JFG_RJgxvVzQ9homV8c5A8cEcAe9B-4zAdM0FunbyjdoztVvD35VCm7EnISuZA8NM_uKN341Egr95Cc7mfSTWHvpXh5uy8mH3RFXwUMOG5fGtFI7GsgQUI2a0oFRVmICBjnpbnO0ZRieOhmS3Mlnj28P3d40UUgbTJBQEFEohTY2icRfaI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/zmku5AIEWfmYC4xb5tgod4P4qeMBUMA2jlzQEjSTmmplf-sQdjPAbNfNR3K9mno1uSeV8KyE3Q4plKPIHhW7JvsXdcZU7r5G8lGXmVyTDlOL6wfGwOfdwNzXRSUU499b29fYjkk4TZ3Jd0O4iHrDBWsU4mZA0zVGxeyl2aeQd2xYwqSVGq4-dQqRB9eMmwUo?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/bfJ2oZsVgj9v3tIWyO5z7vuy97rNLfzoxXJI0AVMFXQU8lv0V7qr1gIj_-v9fGGwDGI5g1b92AXCcAH5x13rdvzHoz270JPZ4BX7WmPoksmUzZ8njRquE1109t7IVpUUXZwA0n8iJmcTuvGazCpkpbMqkL7XHw3uAYBu1eHiQL9FEuhNCwNpLsmNd8Ae8nlL?purpose=fullsize)

## Architecture

```text
Application
    ↓
Metrics
    ↓
Prometheus
    ↓
PromQL
    ↓
Grafana
```

### Important Concepts

- Metrics
- Targets
- Scraping
- Exporters
- PromQL
- Labels
- Time Series
- Alerting
- Alertmanager
- Service Discovery

---

<a id="Grafana"></a>

# 30. Grafana

```text
Prometheus
     ↓
Grafana
     ↓
Dashboard
```

### Important Concepts

- Data Source
- Dashboard
- Panel
- Query
- Variables
- Alert
- Visualization

---

<a id="OpenTelemetry"></a>

# 31. OpenTelemetry

## Three Observability Signals

```text
Logs
Metrics
Traces
```

## Architecture

```text
Application
    ↓
OpenTelemetry
    ↓
Collector
    ↓
Backend
```

### Important Concepts

- Instrumentation
- Collector
- Receiver
- Processor
- Exporter
- Trace
- Span
- Context Propagation

---

====================================

<a id="LGTM-Stack"></a>

# 32. LGTM Stack

```text
L → Loki      → Logs
G → Grafana   → Visualization
T → Tempo     → Traces
M → Mimir     → Metrics
```

### Architecture

```text
Applications
    │
    ├── Logs ─────→ Loki
    ├── Metrics ──→ Mimir
    └── Traces ───→ Tempo
                       ↓
                    Grafana
```

---

<a id="Splunk"></a>

# 33. Splunk

### Important Concepts

- Index
- Search
- SPL
- Forwarder
- Universal Forwarder
- Heavy Forwarder
- Indexer
- Search Head
- Dashboard
- Alert

### Basic SPL

```text
index=application
```

---

<a id="BigPanda"></a>


# 34. BigPanda

### Important Concepts

```text
Monitoring Tools
      ↓
   BigPanda
      ↓
    Events
      ↓
  Correlation
      ↓
   Incident
      ↓
    Alert
```

Know:

- Event
- Alert
- Incident
- Correlation
- Noise Reduction
- Incident Management
- Integration

---

<a id="AI--Development-Tools"></a>

# 35. AI & Development Tools

## AI Tools

- ChatGPT
- GitHub Copilot
- AI-assisted troubleshooting
- AI code generation
- AI documentation
- AI-assisted automation

## Development Tools

- VS Code
- IntelliJ
- Postman
- curl
- Git
- GitHub
- Docker Desktop

---

# Final Quick-Review Priority

## 🔴 Tier 1 — Core DevOps

```text
1. Linux
2. Git
3. GitHub
4. GitHub Actions
5. Docker
6. Kubernetes
7. Kubernetes YAML
8. Terraform
9. AWS
10. Azure
```

## 🟠 Tier 2 — CI/CD & Deployment

```text
11. Jenkins
12. GitLab CI/CD
13. Helm
14. Argo CD
15. Bash/Shell
16. YAML
17. AWS EKS
18. Azure AKS
19. Cloud Networking
20. SSL/TLS
```

## 🟡 Tier 3 — Infrastructure & Operations

```text
21. Ansible
22. Nginx
23. Apache
24. Tomcat
25. JBoss
26. WildFly
27. Prometheus
28. Grafana
29. OpenTelemetry
30. LGTM Stack
31. Splunk
32. BigPanda
```

## 🟢 Tier 4 — Supporting Skills

```text
33. Python
34. JSON
35. AI Tools
36. Development Tools
```

# Complete DevOps Architecture

```text
                         DEVELOPER
                             │
                             ↓
                     Git / GitHub / GitLab
                             │
                             ↓
                       Pull Request
                             │
                       Code Review
                             │
                             ↓
                    CI: Jenkins / Actions
                       / GitLab CI
                             │
                    ┌────────┴────────┐
                    ↓                 ↓
                  Build              Test
                    │                 │
                    └────────┬────────┘
                             ↓
                       Docker Build
                             │
                             ↓
                     ECR / ACR Registry
                             │
                             ↓
                    Helm / Kubernetes
                             │
                    ┌────────┴────────┐
                    ↓                 ↓
                   EKS               AKS
                    │                 │
                    └────────┬────────┘
                             ↓
                         Argo CD
                         GitOps
                             │
                             ↓
                        Production
                             │
              ┌──────────────┼──────────────┐
              ↓              ↓              ↓
          Prometheus       Loki          OpenTelemetry
              ↓              ↓              ↓
           Metrics         Logs           Traces
              │              │              │
              └──────────────┼──────────────┘
                             ↓
                          Grafana
                             │
                             ↓
                    Alerts / BigPanda
```

======================================

# 📅 DevOps & Cloud Roadmap (14 Aug 2025 → 14 Feb 2026)

---

## Month 1–2: Strong Foundation & CI/CD Mastery

### **14 Aug – 27 Aug 2025** ✅

- [✅] Git Basics, Branching & Merging
- [] GitHub / GitLab (VCS basics)
- [ ] Finish Jenkins (advanced pipelines, shared libraries)
- [ ] Start GitLab CI basics
- [ ] YAML & JSON syntax

### **28 Aug – 10 Sep 2025**

- [ ] GitLab CI advanced (runners, caching, artifacts)
- [ ] GitHub Actions basics
- [ ] Shell Scripting (file handling, loops, cron jobs)
- [ ] Docker fundamentals & Docker Compose

### **11 Sep – 24 Sep 2025**

- [ ] Docker networking, volumes, security
- [ ] Kubernetes basics (pods, deployments, services)
- [ ] Helm basics (charts, templates)
- [ ] Terraform basics (provider, variables, state)

---

## Month 3–4: Cloud & Orchestration Expertise

### **25 Sep – 8 Oct 2025**

- [ ] Kubernetes advanced (RBAC, ingress, storage, secrets)
- [ ] AWS core services (EC2, S3, IAM, VPC, CloudWatch)
- [ ] Terraform advanced (modules, workspaces)

### **9 Oct – 22 Oct 2025**

- [ ] Azure basics (VM, Blob, Networking, RBAC)
- [ ] GCP basics (Compute, Storage, IAM)
- [ ] Ansible basics (playbooks, roles, variables)
- [ ] Prometheus & Grafana basics

### **23 Oct – 5 Nov 2025**

- [ ] OpenShift basics (projects, deployment configs)
- [ ] Rancher basics
- [ ] ELK Stack basics
- [ ] Splunk overview

---

## Month 5: Advanced Automation & Observability

### **6 Nov – 19 Nov 2025**

- [ ] ArgoCD & Spinnaker basics
- [ ] Pulumi basics
- [ ] Puppet & Chef overview
- [ ] NGINX basics

### **20 Nov – 3 Dec 2025**

- [ ] Apache basics
- [ ] MySQL & PostgreSQL basics
- [ ] MongoDB basics
- [ ] Linux Administration (user mgmt, networking, services, logs)

---

## Month 6: Interview Prep & Integration

### **4 Dec – 17 Dec 2025**

- [ ] Integrate CI/CD + Terraform + Kubernetes + AWS in a single project
- [ ] Postman API testing basics
- [ ] SonarQube basics (code quality checks)

### **18 Dec – 31 Dec 2025**

- [ ] Jira & ServiceNow usage
- [ ] Build tools: Maven, Gradle, npm basics
- [ ] VS Code, IntelliJ, PyCharm tips for DevOps work

### **1 Jan – 14 Jan 2026**

- [ ] Review all tools — make short notes & cheatsheets
- [ ] Mock projects: Deploy full-stack app via CI/CD on cloud

### **15 Jan – 14 Feb 2026**

- [ ] Full interview preparation for DevOps & Cloud
- [ ] Practice scenario-based questions
- [ ] Revise scripting, Terraform, Kubernetes, and CI/CD flows

---

🔑 Ranked DevOps Skills (2026 Focus)

| Rank   | Skill                                                | Why It Matters                                                                                    | Interview Weight (%) |
| ------ | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------- |
| **1**  | **Linux Fundamentals & Shell Scripting**             | Core of all DevOps work: command-line fluency, process debugging, networking, automation scripts. | **25–30%**           |
| **2**  | **Kubernetes (Production Ops)**                      | Cluster upgrades, RBAC, service mesh, debugging at scale.                                         | **20–25%**           |
| **3**  | **CI/CD Pipeline Design**                            | Jenkins, GitHub Actions, GitLab CI; resilient deployments, rollback strategies.                   | **15–20%**           |
| **4**  | **Cloud Platform Expertise (AWS/GCP/Azure)**         | IAM, networking, storage, managed DBs, serverless.                                                | **15–20%**           |
| **5**  | **Infrastructure as Code (Terraform/Ansible)**       | Module design, state management, multi-env patterns.                                              | **10–15%**           |
| **6**  | **Observability (Prometheus/Grafana/OpenTelemetry)** | Logs, metrics, traces, SLOs, alerting.                                                            | **10–15%**           |
| **7**  | **Incident Response & Troubleshooting**              | Sev-1/Sev-2 handling, postmortems, communication.                                                 | **10–15%**           |
| **8**  | **Networking Fundamentals**                          | TCP/IP, DNS, TLS, load balancers, VPNs.                                                           | **5–10%**            |
| **9**  | **Containerization (Docker)**                        | Image building, orchestration basics, security.                                                   | **5–10%**            |
| **10** | **Soft Skills (Problem-Solving, Communication)**     | Collaboration, explaining trade-offs, handling pressure.                                          | **10–15%**           |

---

## 📌 Common Names of Symbols

- `~` → **Tilde**
- `%` → **Percentage**
- `&` → **And / Ampersand**
- `!` → **Exclamation mark**
- `*` → **Star / Asterisk**
- `@` → **At the rate**
- `#` → **Hash / Number sign**
- `$` → **Dollar sign**
- `^` → **Caret**
- `_` → **Underscore**
- `-` → **Hyphen / Dash**

---
