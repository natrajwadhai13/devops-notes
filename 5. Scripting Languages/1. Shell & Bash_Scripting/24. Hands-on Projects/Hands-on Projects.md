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

If your goal is **Linux Admin / DevOps interviews **, these are the **highest-priority** projects:

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


===========================================


Bilkul. Interview ke liye **bahut advanced script yaad karne ki zarurat nahi hai**. Tumhara target hona chahiye:

> **Input → Check → Condition → Action → Output**

Neeche main 15 projects ko **short + interview-friendly Bash scripts** mein convert kar raha hoon. Inmein almost saare important Bash concepts cover ho jayenge: variables, commands, `if`, `for`, `while`, functions, arguments, exit status, pipes, `grep`, `awk`, `sed`, `curl`, `systemctl`, `df`, `free`, `docker`, `kubectl`, AWS CLI etc.

---

# 1. System Health Check

**Concept:** variables + commands + `if`

```bash
#!/bin/bash

CPU=$(top -bn1 | awk '/Cpu/ {print $2}')
MEM=$(free -m | awk '/Mem/ {print $3}')
DISK=$(df -h / | awk 'NR==2 {print $5}')

echo "CPU Usage: $CPU%"
echo "Memory Used: ${MEM}MB"
echo "Disk Usage: $DISK"

if [ "${DISK%\%}" -gt 80 ]; then
    echo "WARNING: Disk usage is high"
else
    echo "Disk usage is OK"
fi
```

### Interview mein explain:

> "I collect CPU, memory and disk utilization using Linux commands and use an if condition to check whether disk usage is above 80%."

---

# 2. User Creation Automation

**Concept:** input + variable + `useradd` + condition

```bash
#!/bin/bash

read -p "Enter username: " USER

if id "$USER" &>/dev/null; then
    echo "User already exists"
else
    useradd "$USER"
    echo "User $USER created successfully"
fi
```

### Interview explanation

> "First I take the username as input, check whether the user exists using `id`, and create the user using `useradd` if it doesn't exist."

---

# 3. Log File Analyzer

**Concept:** argument + `grep` + `wc`

```bash
#!/bin/bash

LOG=$1

echo "Error count:"
grep -i "error" "$LOG" | wc -l

echo "Warning count:"
grep -i "warning" "$LOG" | wc -l
```

Run:

```bash
./log.sh /var/log/messages
```

### Important concept

`$1` = first command-line argument.

Interview:

> "The script accepts the log file as an argument and counts ERROR and WARNING messages."

---

# 4. Automatic Backup Script

**Concept:** variable + `tar`

```bash
#!/bin/bash

SOURCE="/home/user/data"
BACKUP="/backup/data_$(date +%F).tar.gz"

tar -czf "$BACKUP" "$SOURCE"

echo "Backup completed: $BACKUP"
```

### Interview explanation

> "I create a compressed tar archive and append the current date to the backup filename."

Example:

```text
data_2026-08-27.tar.gz
```

---

# 5. Disk Cleanup Script

**Concept:** `find` + delete

```bash
#!/bin/bash

DIR="/tmp"

find "$DIR" -type f -mtime +7 -delete

echo "Old files deleted"
```

Meaning:

```text
-type f      → files
-mtime +7    → older than 7 days
-delete      → delete
```

Interview:

> "I use find to identify files older than seven days and remove them from the temporary directory."

---

# 6. SSL Certificate Expiry Checker

**Concept:** `openssl` + date calculation

Simple interview version:

```bash
#!/bin/bash

DOMAIN=$1

EXPIRY=$(echo | openssl s_client -connect "$DOMAIN:443" -servername "$DOMAIN" 2>/dev/null |
openssl x509 -noout -enddate)

echo "SSL Certificate: $EXPIRY"
```

Run:

```bash
./ssl.sh google.com
```

### Interview mein:

> "I connect to port 443, extract the SSL certificate and display its expiry date."

**Note:** Interview mein pehle simple version likhna better hai. Agar interviewer bole **"days remaining calculate karo"**, tab calculation add karna.

---

# 7. Docker Container Health Checker

**Concept:** `for` loop + Docker commands

```bash
#!/bin/bash

for CONTAINER in $(docker ps -q); do

    STATUS=$(docker inspect -f '{{.State.Status}}' "$CONTAINER")

    echo "$CONTAINER : $STATUS"

done
```

Output:

```text
abc123 : running
def456 : running
```

Interview:

> "I get running container IDs, inspect their status and print the container health."

---

# 8. Website Monitoring

**Concept:** `curl` + exit status + `if`

```bash
#!/bin/bash

URL="https://google.com"

if curl -s --head "$URL" > /dev/null; then
    echo "Website is UP"
else
    echo "Website is DOWN"
fi
```

### Very important concept

```bash
if command
```

Command successful → `if` true.

Command failed → `else`.

Interview:

> "I use curl to check whether the website is reachable and based on the command exit status I print UP or DOWN."

---

# 9. Service Restart Automation

**Concept:** `systemctl` + condition

```bash
#!/bin/bash

SERVICE="nginx"

if systemctl is-active --quiet "$SERVICE"; then
    echo "$SERVICE is running"
else
    echo "$SERVICE is down"
    systemctl restart "$SERVICE"
    echo "$SERVICE restarted"
fi
```

### Interview explanation

> "I check the service status. If the service is not active, I restart it using systemctl."

This is **very good interview script**.

---

# 10. AWS EC2 Health Check

**Concept:** AWS CLI + loop

```bash
#!/bin/bash

for ID in $(aws ec2 describe-instances \
--query 'Reservations[*].Instances[*].InstanceId' \
--output text); do

    STATE=$(aws ec2 describe-instance-status \
    --instance-ids "$ID" \
    --query 'InstanceStatuses[0].InstanceStatus.Status' \
    --output text)

    echo "$ID : $STATE"

done
```

Interview:

> "I retrieve EC2 instance IDs using AWS CLI and check their instance status."

If interviewer doesn't require exact AWS syntax, explain the logic rather than trying to memorize every `--query`.

---

# 11. Jenkins Build Automation

**Concept:** function + curl

```bash
#!/bin/bash

JENKINS_URL="http://jenkins:8080"
JOB="my-job"

curl -X POST "$JENKINS_URL/job/$JOB/build"

echo "Jenkins build triggered"
```

Interview:

> "I use Jenkins REST API through curl to trigger a build."

---

# 12. Kubernetes Pod Monitoring

**Concept:** `kubectl` + loop + condition

```bash
#!/bin/bash

for POD in $(kubectl get pods -o name); do

    STATUS=$(kubectl get "$POD" -o jsonpath='{.status.phase}')

    echo "$POD : $STATUS"

    if [ "$STATUS" != "Running" ]; then
        echo "WARNING: $POD is not running"
    fi

done
```

Interview:

> "I get all pod names, check their phase and generate a warning when a pod is not running."

---

# 13. Nginx Log Analyzer

**Concept:** `awk` + `sort` + `uniq`

```bash
#!/bin/bash

LOG="/var/log/nginx/access.log"

echo "Top IP addresses:"

awk '{print $1}' "$LOG" |
sort |
uniq -c |
sort -nr |
head
```

### Pipeline samjho:

```text
awk
 ↓
sort
 ↓
uniq
 ↓
sort
 ↓
head
```

Interview:

> "I extract client IPs from the Nginx access log, count them and display the top IP addresses."

---

# 14. CPU & Memory Alert

**Concept:** variables + conditions

```bash
#!/bin/bash

CPU=$(top -bn1 | awk '/Cpu/ {print int($2)}')
MEM=$(free | awk '/Mem/ {printf "%.0f", $3/$2*100}')

if [ "$CPU" -gt 80 ]; then
    echo "ALERT: CPU usage is high"
fi

if [ "$MEM" -gt 80 ]; then
    echo "ALERT: Memory usage is high"
fi
```

Interview:

> "I collect CPU and memory utilization and generate an alert when either crosses 80 percent."

---

# 15. Daily Server Report

**Concept:** variables + multiple commands + output file

```bash
#!/bin/bash

REPORT="/tmp/server_report.txt"

echo "===== SERVER REPORT =====" > "$REPORT"

echo "Hostname:" >> "$REPORT"
hostname >> "$REPORT"

echo "Uptime:" >> "$REPORT"
uptime >> "$REPORT"

echo "Disk Usage:" >> "$REPORT"
df -h >> "$REPORT"

echo "Memory:" >> "$REPORT"
free -h >> "$REPORT"

echo "Report generated: $REPORT"
```

Interview:

> "I collect hostname, uptime, disk and memory information and store the output in a report file."

---

# ⭐ Ab sab scripts ka Common Pattern

Actually **15 scripts alag-alag yaad karne ki zarurat nahi hai.**

Bas ye structure yaad rakho:

```bash
#!/bin/bash

# 1. Input / Variable
VALUE="something"

# 2. Command
RESULT=$(command)

# 3. Check
if [ "$RESULT" == "something" ]; then
    echo "Success"
else
    echo "Failure"
fi

# 4. Action
command

# 5. Output
echo "Done"
```

Is pattern se tum bahut saare interview questions bana sakte ho.

---

# 🧠 Bash Interview ke 10 Concepts — Ye Pakka Karo

| Concept        | Example               |
| -------------- | --------------------- |
| Variable       | `NAME="natraj"`       |
| User input     | `read -p`             |
| Argument       | `$1`                  |
| Command output | `$(command)`          |
| If/else        | `if [ ]; then`        |
| For loop       | `for x in ...`        |
| While loop     | `while ...`           |
| Function       | `function_name() { }` |
| Pipe           | `command \| grep`     |
| Exit status    | `$?`                  |

### Aur ye commands strong karo:

```bash
grep
awk
sed
cut
sort
uniq
wc
find
xargs
df
du
free
ps
top
systemctl
journalctl
curl
tar
ssh
scp
```

---

# 🔥 Interview mein agar bole: "Write a Shell Script"

Sabse pehle **problem ko 4 parts mein todna**:

```text
1. Input kya hai?
        ↓
2. Kya check karna hai?
        ↓
3. Condition kya hai?
        ↓
4. Action kya lena hai?
```

Example interviewer:

> "Write a script to check whether nginx is running."

Tum immediately socho:

```text
Input       → nginx
Check       → systemctl
Condition   → running / not running
Action      → restart
Output      → message
```

Then:

```bash
#!/bin/bash

SERVICE="nginx"

if systemctl is-active --quiet "$SERVICE"; then
    echo "$SERVICE is running"
else
    echo "$SERVICE is down"
    systemctl restart "$SERVICE"
fi
```

**Bas.** Interview mein unnecessarily 50-line production-level script likhne ki zarurat nahi.

---

## 🎯 Tumhare liye Best Learning Order

Tumne Bash pehle padha hua hai aur ab interview preparation ke liye wapas start kar rahe ho, isliye main is order mein practice karne ko bolunga:

**Level 1 — Basic**

```text
Variables
read
echo
$1
if/else
```

↓

**Level 2 — Commands**

```text
grep
awk
sed
cut
sort
wc
find
```

↓

**Level 3 — Loops**

```text
for
while
```

↓

**Level 4 — Functions**

```text
function
return
```

↓

**Level 5 — DevOps Scripts**

```text
System Health
User Creation
Backup
Log Analyzer
Docker
Jenkins
AWS
Kubernetes
```
