---
title: "24. Hands-on Projects"
nav_order: 24
parent: "• Shell & Bash_Scripting"
grand_parent: "5. Scripting Languages"
---

## Hands-on Projects

1. System Health Check Script
2. User Creation Automation
3. Log File Analyzer
4. Automatic Backup Script
5. Disk Cleanup Script
6. SSL Certificate Expiry Checker
7. Docker Container Health Checker
8. Website Monitoring Script
9. Service Restart Automation
10. AWS EC2 Health Check Script
11. Jenkins Build Automation
12. Kubernetes Pod Monitoring Script
13. Nginx Log Analyzer
14. CPU & Memory Alert Script
15. Daily Server Report Generator

---

This is an excellent **Hands-on Projects** section. Since you're preparing for **Linux Admin + DevOps (7+ years experience)** interviews, I'd make it slightly more industry-focused.

---

# Hands-on Projects

## Beginner Level ⭐

### 1. System Health Check Script

Topics Covered

- Disk Usage
- Memory Usage
- CPU Usage
- Load Average
- Uptime
- Hostname
- Date & Time
- Running Services

Commands

```text
df
free
uptime
hostname
date
systemctl
```

---

### 2. User Creation Automation

Topics

- Create User
- Set Password
- Add Group
- Home Directory
- User Validation

Commands

```text
useradd
passwd
groupadd
usermod
id
```

---

### 3. Log File Analyzer

Topics

- Count ERROR
- Count WARNING
- Search Keywords
- Top 10 Errors
- Date-wise Logs

Commands

```text
grep
awk
sed
sort
uniq
wc
```

---

### 4. Automatic Backup Script

Topics

- Copy Files
- Compress Files
- Timestamp Backup
- Backup Rotation
- Logging

Commands

```text
cp
tar
gzip
date
find
```

---

### 5. Disk Cleanup Script

Topics

- Delete Old Logs
- Remove Temp Files
- Delete Empty Files
- Clean Cache

Commands

```text
find
rm
du
```

---

# Intermediate Level ⭐⭐

### 6. SSL Certificate Expiry Checker

Topics

- Domain Validation
- SSL Expiry Date
- Days Remaining
- Email Alert

Commands

```text
openssl
date
mail
```

---

### 7. Docker Container Health Checker

Topics

- Running Containers
- Restart Failed Containers
- Container Logs
- Resource Usage

Commands

```text
docker ps
docker inspect
docker restart
docker logs
```

---

### 8. Website Monitoring Script

Topics

- HTTP Status
- Response Time
- Ping Check
- Email Notification

Commands

```text
curl
ping
mail
logger
```

---

### 9. Service Restart Automation

Topics

- Service Status
- Restart Failed Service
- Logging
- Retry Mechanism

Commands

```text
systemctl
logger
```

---

### 10. AWS EC2 Health Check Script

Topics

- CPU
- Memory
- Disk
- Instance Metadata
- Network

Commands

```text
curl
df
free
uptime
hostname
```

---

### 11. Jenkins Build Automation

Topics

- Pull Code
- Build Project
- Deploy
- Log Output

Commands

```text
git
mvn
docker
kubectl
```

---

# Advanced Level ⭐⭐⭐

### 12. Kubernetes Pod Monitoring Script

Topics

- Pod Status
- CrashLoopBackOff Detection
- Restart Count
- Namespace Report

Commands

```text
kubectl
grep
awk
```

---

### 13. Nginx Log Analyzer

Topics

- Top IP Addresses
- Top URLs
- HTTP Status Codes
- 404 Errors
- 500 Errors

Commands

```text
awk
sort
uniq
grep
```

---

### 14. CPU & Memory Alert Script

Topics

- CPU Threshold
- Memory Threshold
- Email Alert
- Logger
- Cron Job

Commands

```text
top
free
mail
logger
```

---

### 15. Daily Server Report Generator

Topics

- Hostname
- Date
- Uptime
- CPU
- Memory
- Disk
- Services
- Network
- Logged-in Users

Commands

```text
hostname
date
uptime
df
free
ps
ss
who
```

---

# Bonus Projects (Highly Recommended for DevOps Interviews)

### 16. SSL Auto-Renew Checker

- Check Let's Encrypt expiry
- Auto-renew validation
- Restart Nginx after renewal

---

### 17. Docker Image Cleanup Automation

- Remove dangling images
- Remove unused containers
- Remove unused volumes
- Remove unused networks

---

### 18. Kubernetes Namespace Health Report

- Pods
- Deployments
- Services
- PVC
- Nodes
- Events

---

### 19. Git Auto Deployment Script

- Git Pull
- Build
- Docker Build
- Docker Push
- Kubernetes Deploy
- Health Check

---

### 20. Complete DevOps Deployment Script

```text
Git Pull
      │
      ▼
Build
      │
      ▼
Docker Build
      │
      ▼
Docker Push
      │
      ▼
Kubernetes Deploy
      │
      ▼
Health Check
      │
      ▼
Rollback (if failed)
```

---

# Project Difficulty Roadmap

| Level             | Projects |
| ----------------- | -------- |
| ⭐ Beginner       | 1–5      |
| ⭐⭐ Intermediate | 6–11     |
| ⭐⭐⭐ Advanced   | 12–15    |
| 🚀 Expert         | 16–20    |

## Interview Priority

If your goal is **Linux Admin / DevOps interviews (15–25 LPA)**, these are the **highest-priority** projects:

1. ✅ System Health Check Script
2. ✅ Automatic Backup Script
3. ✅ Log File Analyzer
4. ✅ Website Monitoring Script
5. ✅ Service Restart Automation
6. ✅ Docker Container Health Checker
7. ✅ CPU & Memory Alert Script
8. ✅ Nginx Log Analyzer
9. ✅ Kubernetes Pod Monitoring Script
10. ✅ Complete DevOps Deployment Script

These ten projects cover most of the practical scripting scenarios commonly discussed in Linux Administrator, DevOps, and SRE interviews.
