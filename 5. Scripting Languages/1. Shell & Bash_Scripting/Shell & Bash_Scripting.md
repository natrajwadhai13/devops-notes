---
title: "• Shell & Bash_Scripting"
parent: "5. Scripting Languages"
nav_order: 1
has_children: true
---

## Complete Shell Scripting / Bash Scripting Syllabus (DevOps Focus)

**Shell Scripting and Bash Scripting together**. In practice, most Linux systems use **Bash**, so the terms are often used interchangeably. Bash is simply the most popular shell used for shell scripting.

### Module 1: Introduction

- What is Shell?
- What is Bash?
- Types of Shells (sh, bash, ksh, zsh)
- Shell vs Bash
- Why Shell Scripting?
- Real-world automation examples

---

### Module 2: Script Basics

- First Shell Script
- Shebang (`#!/bin/bash`)
- Comments
- Execute Script
- chmod +x
- bash script.sh vs ./script.sh
- Exit Status (`$?`)

---

### Module 3: Variables

- User Variables
- Environment Variables
- Read-only Variables
- Export Variables
- Special Variables
  - `$0`
  - `$1-$9`
  - `$#`
  - `$*`
  - `$@`
  - `$$`
  - `$?`
  - `$!`

---

### Module 4: User Input

- read command
- Prompt message
- Hidden Password (`read -s`)
- Multiple Inputs
- Default Values

---

### Module 5: Operators

- Arithmetic
- Comparison
- String
- Logical
- File Test Operators

---

### Module 6: Conditional Statements

- if
- if-else
- elif
- Nested if
- test command
- `[ ]`
- `[[ ]]`
- case statement

---

### Module 7: Loops

- for loop
- while loop
- until loop
- Infinite Loop
- break
- continue

---

### Module 8: Functions

- Function Declaration
- Return Values
- Local Variables
- Passing Arguments
- Recursive Functions

---

### Module 9: Arrays

- Indexed Arrays
- Associative Arrays
- Array Operations
- Loop Through Arrays

---

### Module 10: Strings

- String Length
- Concatenation
- Substring
- Replace Text
- Uppercase
- Lowercase
- Pattern Matching

---

### Module 11: File Handling

- Check File Exists
- Create/Delete Files
- Read File
- Write File
- Append File
- Permissions
- File Size
- Backup Script

---

### Module 12: Command Line Arguments

- Positional Parameters
- shift
- getopts
- Option Parsing

---

### Module 13: Input / Output

- stdin
- stdout
- stderr
- Redirection (`>`, `>>`, `<`, `2>`)
- Pipe (`|`)
- tee

---

### Module 14: Text Processing

- grep
- egrep
- cut
- awk
- sed
- sort
- uniq
- tr
- wc
- head
- tail
- xargs
- find

---

### Module 15: Process Management

- ps
- top
- kill
- killall
- jobs
- bg
- fg
- nohup
- nice

---

### Module 16: System Administration Scripts

- User Creation
- Password Reset
- User Deletion
- Group Management
- Disk Usage Report
- Memory Report
- CPU Monitoring
- Service Status

---

### Module 17: Logging & Debugging

- set -x
- set -e
- set -v
- trap
- Logger
- Error Handling

---

### Module 18: Scheduling

- cron
- crontab
- at command
- Automated Jobs

---

### Module 19: Regular Expressions

- Regex Basics
- grep Regex
- sed Regex
- awk Regex

---

### Module 20: Networking Scripts

- ping
- ssh
- scp
- curl
- wget
- netstat
- ss
- nc (Netcat)

---

### Module 21: DevOps Automation

- Git Automation
- Docker Automation
- Kubernetes Automation
- Jenkins Script
- Backup Script
- Health Check Script
- Deployment Script

---

### Module 22: Advanced Bash

- Command Substitution
- Arithmetic Expansion
- Brace Expansion
- Process Substitution
- Here Document
- Here String
- Source Command
- Alias
- Shell Options
- Trap Signals
- Named Pipes

---

### Module 23: Best Practices

- Coding Standards
- Script Structure
- Error Handling
- Logging
- Reusable Functions
- Secure Scripting
- Performance Optimization

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

## Interview Topics

- Shell vs Bash
- Shebang
- Special Variables
- Difference between `$*` and `$@`
- Difference between `[` and `[[`
- if vs case
- for vs while
- Arrays
- Functions
- getopts
- sed vs awk
- grep vs egrep
- Exit Codes
- Cron Jobs
- Debugging
- Trap Command
- File Descriptors
- Redirection
- Pipes
- Process Management
- Shell Script Best Practices

For your **DevOps GitHub roadmap**, this syllabus is enough to cover **95% of the Bash/Shell scripting knowledge** expected in Linux Administrator, DevOps Engineer, SRE, and Cloud Engineer interviews.

- [Bash Scripting Fundamentals | Linuxize](https://linuxize.com/series/bash-scripting-fundamentals/?utm_source=chatgpt.com)

===========================================

# ⭐⭐⭐⭐⭐ Must Know (Very Important)

Ye topics lagbhag har interview me pooche ja sakte hain.

1. Variables & Export Variables
2. Command Line Arguments (`$1`, `$2`, `$#`, `$@`, `$*`)
3. Exit Status (`$?`)
4. if / else / elif
5. case Statement
6. for Loop
7. while Loop
8. Functions
9. Arrays
10. File Test Operators (`-f`, `-d`, `-r`, `-w`, `-x`)
11. String Operations
12. grep
13. sed
14. awk (Basic)
15. cut
16. sort
17. uniq
18. head / tail / wc
19. Pipes (`|`)
20. Input/Output Redirection (`>`, `>>`, `2>`, `/dev/null`)
21. Command Substitution (`$( )`)
22. Arithmetic Expansion (`$(( ))`)
23. Here Document (`<<EOF`)
24. File Handling
25. Debugging (`set -x`, `set -e`)
26. crontab
27. Backup Script
28. Process Monitoring Script
29. Disk Usage Script
30. Log Cleanup Script

---

# ⭐⭐⭐⭐ Important

1. break / continue
2. until Loop
3. Associative Arrays
4. tee
5. trap
6. nohup
7. jobs / bg / fg
8. xargs
9. find with `-exec`
10. Source Command (`source`)
11. `.bashrc`
12. Environment Variables
13. `getopts`
14. Regex Basics

---

# ⭐⭐⭐ Medium

1. Process Substitution
2. Here String
3. Recursive Functions
4. at Command
5. Aliases
6. `.bash_profile`
7. Log Rotation

---

# ⭐⭐ Rarely Asked

1. Brace Expansion
2. Advanced Regex
3. Complex `awk`
4. `exec`
5. Nested Loops
6. Recursive Bash Scripts

---

## Agar sirf Top 15 padhna ho to

1. Variables & Export
2. Command Line Arguments
3. if-else
4. for Loop
5. while Loop
6. Functions
7. Arrays
8. grep
9. sed
10. awk (Basic)
11. Redirection & Pipes
12. File Handling
13. crontab
14. `$( )` Command Substitution
15. Backup Script

=========================================================

---

## 🧭 Bash Roadmap for DevOps Engineers (3–4 Weeks)


---

## 🔰 **Week 1: Core Bash Fundamentals**

### 🎯 Outcomes:

- Understand Bash syntax, variables, conditionals, and loops

### Topics:

- Shebang (`#!/bin/bash`)
- Variables (`name="natraj"`)
- Quoting: `" "$var" vs '$var'`
- `echo`, `read`, `printf`
- Conditional statements:
  - `if`, `else`, `elif`, `case`

- Loops:
  - `for`, `while`, `until`

- Exit codes and `$?`

### 🧪 Sample Script:

```bash
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

---

## 🔧 Week 2: Intermediate Scripting + File/Process Management

### 🎯 Outcomes:

- Write reusable scripts for tasks like monitoring, backups, automation

### Topics:

- Functions in Bash
- Arguments: `$1`, `$2`, `$@`, `$#`
- File test operators (`-f`, `-d`, `-e`)
- String and arithmetic operations
- Loops with files
- Scheduling with `cron`
- Working with `find`, `grep`, `awk`, `sed`, `cut`, `xargs`

### 🧪 Sample Script (Backup):

```bash
#!/bin/bash
src="/etc/nginx/"
dest="/backup/nginx_$(date +%F).tar.gz"

tar -czf $dest $src
echo "Backup saved to $dest"
```

---

## ⚙️ Week 3: DevOps + Automation Use Cases

### 🎯 Outcomes:

- Use Bash in real DevOps environments

### Topics:

- Automation with `scp`, `ssh`, `rsync`
- Parse logs and monitor services
- Service status check scripts
- Bash with AWS CLI (`aws s3`, `aws ec2`, etc.)
- Bash with Docker (`docker ps`, `docker inspect`)
- Bash with Git (`git pull`, `git clone` automation)

### 🧪 Sample: Service Health Check

```bash
#!/bin/bash
services=("nginx" "docker" "sshd")

for s in "${services[@]}"; do
  if systemctl is-active --quiet $s; then
    echo "$s is running"
  else
    echo "$s is NOT running"
  fi
done
```

---

## 📦 Week 4: Advanced Bash + Integration with DevOps Tools

### 🎯 Outcomes:

- Master Bash for complex pipelines, hooks, and jobs

### Topics:

- Bash in Jenkins `sh` step
- Bash in Git hooks (pre-commit, post-merge)
- Bash in Terraform & Ansible (external scripts)
- Error handling with `trap`, `set -e`, `set -x`
- Logging, color outputs, exit traps

### 🧪 Sample: Jenkins Build Step

```bash
pipeline {
  agent any
  stages {
    stage('Run Bash') {
      steps {
        sh '''
          echo "Running deployment..."
          ./deploy.sh
        '''
      }
    }
  }
}
```

---

## 📘 Must-Learn Bash Commands for DevOps

| Command | Use Case                    |
| ------- | --------------------------- |
| `grep`  | Search logs, errors         |
| `awk`   | Field extraction, reporting |
| `sed`   | Stream editing              |
| `cut`   | Column extraction           |
| `xargs` | Process lists efficiently   |
| `curl`  | REST APIs and integrations  |
| `jq`    | JSON parsing with Bash      |

---

## 🧪 Mini Projects for Practice

1. **Disk space monitor script with alert email**
2. **Automate log archive rotation**
3. **Docker container health check via cron**
4. **S3 backup automation using AWS CLI + cron**
5. **Create Jenkins pipeline with custom Bash scripts**

---

## 🧠 Bash Best Practices

- Use `set -e` to fail fast
- Validate all inputs (`if [[ -z $var ]]`)
- Modularize using functions
- Avoid hardcoding paths — use variables
- Always test scripts with `bash -x script.sh`

---

## 📚 Useful Resources

- [Explainshell.com](https://explainshell.com/) – explains bash commands
- [ShellCheck](https://www.shellcheck.net/) – bash script linter
- [tldr.sh](https://tldr.sh) – simplified bash command docs


