---
title: "• System-Health-Check-Script"
nav_order: 1
parent: "24. Hands-on Projects"
grand_parent: "• Shell & Bash_Scripting"
grand_grand_parent: "5. Scripting Languages"
---

# System Health Check Script — Advanced Bash

For an **advanced-level DevOps Bash project**, don't make the script only print `df`, `free`, and `uptime`. It should behave like a real monitoring utility:

### Features

* Hostname and OS information
* Uptime and load average
* CPU utilization
* Memory utilization
* Disk utilization
* Top CPU-consuming processes
* Top memory-consuming processes
* Network/listening ports
* Important service status
* Root filesystem check
* Threshold-based warnings
* Logging
* Exit codes
* Colorized terminal output
* `set -euo pipefail`
* Functions
* Command validation
* `trap` cleanup
* Optional email/alert integration

---

## Project Structure

```text
system-health-check/
├── health_check.sh
├── health_check.log
└── README
```

---

## Advanced Script

```bash
#!/bin/bash

set -euo pipefail

# ==========================================================
# System Health Check Script
# ==========================================================

# -----------------------------
# Configuration
# -----------------------------

HOSTNAME=$(hostname)
LOG_FILE="/var/log/system_health.log"

CPU_THRESHOLD=80
MEMORY_THRESHOLD=80
DISK_THRESHOLD=80

SERVICES=("sshd" "docker")

# -----------------------------
# Colors
# -----------------------------

RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m'

# -----------------------------
# Functions
# -----------------------------

log() {

    local level="$1"
    local message="$2"

    echo "$(date '+%Y-%m-%d %H:%M:%S') [$level] $message" \
        | tee -a "$LOG_FILE"

}

info() {

    log "INFO" "$1"

}

warning() {

    echo -e "${YELLOW}[WARNING] $1${NC}"
    log "WARNING" "$1"

}

success() {

    echo -e "${GREEN}[OK] $1${NC}"
    log "INFO" "$1"

}

error() {

    echo -e "${RED}[ERROR] $1${NC}"
    log "ERROR" "$1"

}

check_command() {

    local command_name="$1"

    if ! command -v "$command_name" >/dev/null 2>&1
    then

        error "Required command not found: $command_name"

        return 1

    fi

}

cleanup() {

    info "Health check completed."

}

trap cleanup EXIT

# -----------------------------
# Check Required Commands
# -----------------------------

check_dependencies() {

    local commands=(
        awk
        df
        free
        uptime
        ps
        systemctl
    )

    for command in "${commands[@]}"
    do

        check_command "$command" || return 1

    done

}

# -----------------------------
# System Information
# -----------------------------

system_info() {

    echo
    echo "=========================================="
    echo "        SYSTEM HEALTH CHECK"
    echo "=========================================="

    echo "Hostname       : $HOSTNAME"

    echo "Date           : $(date)"

    echo "Kernel         : $(uname -r)"

    echo "OS             : $(grep '^PRETTY_NAME=' /etc/os-release \
        | cut -d= -f2- | tr -d '"')"

    echo "Uptime         : $(uptime -p)"

    echo "Load Average   : $(awk '{print $1,$2,$3}' /proc/loadavg)"

    echo "=========================================="

}

# -----------------------------
# CPU Check
# -----------------------------

check_cpu() {

    echo
    echo "---------- CPU ----------"

    local cpu_usage

    cpu_usage=$(
        top -bn1 |
        awk '/Cpu\(s\)/ {
            print 100 - $8
        }'
    )

    cpu_usage=${cpu_usage%.*}

    echo "CPU Usage      : ${cpu_usage}%"

    if (( cpu_usage >= CPU_THRESHOLD ))
    then

        warning "High CPU usage: ${cpu_usage}%"

    else

        success "CPU usage normal: ${cpu_usage}%"

    fi

}

# -----------------------------
# Memory Check
# -----------------------------

check_memory() {

    echo
    echo "---------- MEMORY ----------"

    local memory_usage

    memory_usage=$(
        free |
        awk '/Mem:/ {
            printf "%.0f", ($3/$2)*100
        }'
    )

    echo "Memory Usage   : ${memory_usage}%"

    if (( memory_usage >= MEMORY_THRESHOLD ))
    then

        warning "High memory usage: ${memory_usage}%"

    else

        success "Memory usage normal: ${memory_usage}%"

    fi

}

# -----------------------------
# Disk Check
# -----------------------------

check_disk() {

    echo
    echo "---------- DISK ----------"

    while read -r filesystem usage mount
    do

        usage=${usage%\%}

        echo "$mount : ${usage}%"

        if (( usage >= DISK_THRESHOLD ))
        then

            warning "High disk usage on $mount: ${usage}%"

        else

            success "Disk usage normal on $mount: ${usage}%"

        fi

    done < <(
        df -hP |
        awk 'NR>1 {print $1,$5,$6}'
    )

}

# -----------------------------
# Top CPU Processes
# -----------------------------

top_cpu_processes() {

    echo
    echo "---------- TOP CPU PROCESSES ----------"

    ps -eo pid,user,comm,%cpu --sort=-%cpu |
        head -n 6

}

# -----------------------------
# Top Memory Processes
# -----------------------------

top_memory_processes() {

    echo
    echo "---------- TOP MEMORY PROCESSES ----------"

    ps -eo pid,user,comm,%mem --sort=-%mem |
        head -n 6

}

# -----------------------------
# Service Check
# -----------------------------

check_services() {

    echo
    echo "---------- SERVICES ----------"

    for service in "${SERVICES[@]}"
    do

        if systemctl is-active --quiet "$service"
        then

            success "$service is running"

        else

            error "$service is NOT running"

        fi

    done

}

# -----------------------------
# Network Check
# -----------------------------

network_check() {

    echo
    echo "---------- NETWORK ----------"

    if command -v ss >/dev/null 2>&1
    then

        echo "Listening Ports:"

        ss -tuln

    else

        warning "ss command not available"

    fi

}

# -----------------------------
# Root Filesystem
# -----------------------------

root_filesystem_check() {

    echo
    echo "---------- ROOT FILESYSTEM ----------"

    local root_usage

    root_usage=$(
        df -P / |
        awk 'NR==2 {
            gsub("%","",$5);
            print $5
        }'
    )

    echo "Root Usage     : ${root_usage}%"

    if (( root_usage >= DISK_THRESHOLD ))
    then

        warning "Root filesystem usage is high"

    else

        success "Root filesystem usage is normal"

    fi

}

# -----------------------------
# Main
# -----------------------------

main() {

    check_dependencies

    system_info

    check_cpu

    check_memory

    check_disk

    root_filesystem_check

    top_cpu_processes

    top_memory_processes

    check_services

    network_check

    echo
    echo "=========================================="
    echo "       HEALTH CHECK COMPLETED"
    echo "=========================================="

}

main
```

## Make It Executable

```bash
chmod +x health_check.sh
```

Run:

```bash
sudo ./health_check.sh
```

---

# Important Advanced Concepts Used

### 1. `set -euo pipefail`

```bash
set -euo pipefail
```

This gives the script safer behavior:

```text
-e          Exit when a command fails
-u          Error when using an undefined variable
pipefail    Pipeline fails if any command fails
```

---

### 2. Functions

Instead of putting everything into one long script:

```bash
check_cpu
check_memory
check_disk
check_services
```

Each task has its own function.

This makes the script:

* Reusable
* Readable
* Easier to troubleshoot
* Easier to modify

---

### 3. Arrays

```bash
SERVICES=("sshd" "docker")
```

Then:

```bash
for service in "${SERVICES[@]}"
do
    systemctl is-active "$service"
done
```

You can easily add another service:

```bash
SERVICES=("sshd" "docker" "nginx")
```

---

### 4. Process Substitution

This is an advanced Bash feature:

```bash
while read -r filesystem usage mount
do
    ...
done < <(df -hP | awk 'NR>1 {print $1,$5,$6}')
```

The output of the command is treated like a file.

---

### 5. `local`

Inside functions:

```bash
local cpu_usage
```

This prevents unnecessary modification of global variables.

---

### 6. `trap`

```bash
trap cleanup EXIT
```

The cleanup function runs automatically when the script exits.

This is especially useful for:

* Temporary files
* Lock files
* Cleanup
* Logging
* Graceful termination

---

# Example Output

```text
==========================================
        SYSTEM HEALTH CHECK
==========================================

Hostname       : devops-server
Date           : Thu Aug 27 20:30:10 IST 2026
Kernel         : 5.14.0
OS             : Red Hat Enterprise Linux 9.6
Uptime         : up 5 days, 4 hours
Load Average   : 0.35 0.28 0.22

---------- CPU ----------
CPU Usage      : 35%
[OK] CPU usage normal: 35%

---------- MEMORY ----------
Memory Usage   : 62%
[OK] Memory usage normal: 62%

---------- DISK ----------
/ : 67%
[OK] Disk usage normal on /: 67%

---------- SERVICES ----------
[OK] sshd is running
[OK] docker is running

---------- NETWORK ----------
Listening Ports:
22
80
443

==========================================
       HEALTH CHECK COMPLETED
==========================================
```

# Make It Production-Level

The next step would be to add:

```text
System Health Check
        │
        ├── CPU threshold
        ├── Memory threshold
        ├── Disk threshold
        ├── Service failure
        ├── Network connectivity
        ├── Port check
        ├── SSL certificate expiry
        ├── Log error count
        ├── Docker health
        ├── Kubernetes health
        ├── Email/Slack alert
        ├── HTML report
        └── Cron automation
```

===========================================================


# Basic Version

```bash
#!/bin/bash

echo "===== System Health Check ====="

# Hostname
echo "Hostname: $(hostname)"

# Uptime
echo "Uptime: $(uptime -p)"

# Disk Usage
DISK=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Disk Usage: $DISK%"

if [ "$DISK" -gt 80 ]
then
    echo "WARNING: Disk usage is high"
else
    echo "Disk usage is normal"
fi

# Memory
echo
echo "Memory Usage:"
free -h

# CPU
echo
echo "CPU Load:"
uptime

# Service
SERVICE="sshd"

if systemctl is-active --quiet "$SERVICE"
then
    echo "$SERVICE is running"
else
    echo "$SERVICE is not running"
fi

echo
echo "===== Health Check Completed ====="

```

```bash
| Concept              | Example                |
| -------------------- | ---------------------- |
| Shebang              | `#!/bin/bash`          |
| Variable             | `DISK=...`             |
| Command substitution | `$(df /)`              |
| `awk`                | Extract value          |
| `tr`                 | Remove `%`             |
| `if`                 | Check threshold        |
| Comparison           | `-gt`                  |
| Command              | `free`, `df`, `uptime` |
| Service check        | `systemctl`            |
```

### Explain your script

This script is used to perform a basic server health check. First, I check the hostname and uptime. Then I check memory and disk usage. I use df to get disk utilization and awk to extract the percentage. I store that value in a variable and use an if condition to check whether disk usage is above 80 percent.