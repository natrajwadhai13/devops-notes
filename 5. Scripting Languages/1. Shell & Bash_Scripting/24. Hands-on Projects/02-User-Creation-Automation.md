---
title: "• User-Creation-Automation"
nav_order: 2
parent: "24. Hands-on Projects"
grand_parent: "• Shell & Bash_Scripting"
grand_grand_parent: "5. Scripting Languages"
---

Yes. For **User Creation Automation**, advanced ka matlab unnecessary complex script nahi hona chahiye. Interview mein likhne aur explain karne layak **practical advanced version** banana better hai.

# User Creation Automation — Advanced Bash

### Requirements

Script should:

* Accept username from command line
* Check whether user already exists
* Create user
* Create home directory
* Create group
* Add user to group
* Set password
* Force password change
* Set shell
* Validate input
* Check required commands
* Log activity
* Handle errors

---

## Advanced Interview-Friendly Script

```bash
#!/bin/bash

# User Creation Automation

LOG_FILE="/var/log/user_creation.log"
GROUP="developers"
SHELL="/bin/bash"

# Check root user
if [ "$EUID" -ne 0 ]
then
    echo "ERROR: Please run this script as root."
    exit 1
fi

# Check username argument
if [ $# -ne 1 ]
then
    echo "Usage: $0 <username>"
    exit 1
fi

USERNAME="$1"

# Validate username
if [[ ! "$USERNAME" =~ ^[a-zA-Z0-9._-]+$ ]]
then
    echo "ERROR: Invalid username."
    exit 1
fi

# Check if user already exists
if id "$USERNAME" &>/dev/null
then
    echo "ERROR: User '$USERNAME' already exists."
    exit 1
fi

# Create group if it does not exist
if ! getent group "$GROUP" &>/dev/null
then
    groupadd "$GROUP"

    if [ $? -ne 0 ]
    then
        echo "ERROR: Failed to create group."
        exit 1
    fi
fi

# Create user
useradd \
    -m \
    -s "$SHELL" \
    -g "$GROUP" \
    "$USERNAME"

if [ $? -ne 0 ]
then
    echo "ERROR: Failed to create user."
    exit 1
fi

# Set password
echo "Set password for $USERNAME:"
passwd "$USERNAME"

if [ $? -ne 0 ]
then
    echo "ERROR: Password setup failed."
    exit 1
fi

# Force password change on first login
chage -d 0 "$USERNAME"

# Log successful creation
echo "$(date '+%Y-%m-%d %H:%M:%S') User '$USERNAME' created" \
    >> "$LOG_FILE"

echo
echo "================================"
echo "User Created Successfully"
echo "================================"

echo "Username : $USERNAME"
echo "Group    : $GROUP"
echo "Shell    : $SHELL"
echo "Home     : /home/$USERNAME"

echo
id "$USERNAME"

echo
echo "User must change password on first login."
```

---

# How to Run

Save:

```bash
user_create.sh
```

Make executable:

```bash
chmod +x user_create.sh
```

Run as root:

```bash
sudo ./user_create.sh natraj
```

---

# Example Output

```text
Set password for natraj:
New password:
Retype new password:

================================
User Created Successfully
================================

Username : natraj
Group    : developers
Shell    : /bin/bash
Home     : /home/natraj

uid=1001(natraj) gid=1001(developers) groups=1001(developers)

User must change password on first login.
```

---

# Understand the Script Step-by-Step

## 1. Check Root

```bash
if [ "$EUID" -ne 0 ]
then
    echo "Please run as root"
    exit 1
fi
```

User creation requires administrative privileges.

---

## 2. Command-Line Argument

```bash
if [ $# -ne 1 ]
then
    echo "Usage: $0 <username>"
    exit 1
fi
```

Run:

```bash
./user_create.sh natraj
```

Here:

```text
$0 = ./user_create.sh
$1 = natraj
$# = 1
```

---

## 3. Store Username

```bash
USERNAME="$1"
```

Now instead of repeatedly using `$1`, we use:

```bash
"$USERNAME"
```

---

## 4. Validate Username

```bash
if [[ ! "$USERNAME" =~ ^[a-zA-Z0-9._-]+$ ]]
```

This prevents invalid characters from being used as a username.

For example:

```text
natraj       → Valid
natraj123    → Valid
natraj.dev   → Valid
natraj@123   → Invalid
```

---

# 5. Check Existing User

```bash
if id "$USERNAME" &>/dev/null
then
    echo "User already exists"
    exit 1
fi
```

`id` checks whether the user exists.

---

# 6. Create Group

```bash
if ! getent group "$GROUP" &>/dev/null
then
    groupadd "$GROUP"
fi
```

If `developers` doesn't exist, it creates it.

---

# 7. Create User

Main command:

```bash
useradd -m -s /bin/bash -g developers natraj
```

Options:

| Option | Meaning               |
| ------ | --------------------- |
| `-m`   | Create home directory |
| `-s`   | Set login shell       |
| `-g`   | Set primary group     |

So:

```bash
useradd -m -s /bin/bash -g "$GROUP" "$USERNAME"
```

---

# 8. Set Password

```bash
passwd "$USERNAME"
```

The administrator enters the password interactively.

---

# 9. Force Password Change

```bash
chage -d 0 "$USERNAME"
```

This forces the user to change the password during the first login.

---

# 10. Logging

```bash
echo "$(date '+%Y-%m-%d %H:%M:%S') User '$USERNAME' created" \
    >> "$LOG_FILE"
```

Example:

```text
2026-08-27 20:45:10 User 'natraj' created
```

---

# Interview Explanation

If interviewer asks:

**"Explain your user creation script."**

You can answer:

> "This script automates Linux user creation. First, it checks whether the script is running with root privileges. Then it accepts the username as a command-line argument and validates it. It checks whether the user already exists. If the required group doesn't exist, it creates the group. Then it creates the user with a home directory, Bash shell, and primary group. After that, it sets the password and forces the user to change it during the first login. Finally, it logs the user creation activity."

That's a **strong interview explanation** without being unnecessarily complicated.

---

# Interviewer May Ask: "What if I want to create multiple users?"

Then modify the script:

```bash
for USERNAME in "$@"
do

    echo "Creating user: $USERNAME"

    useradd -m -s /bin/bash "$USERNAME"

done
```

Run:

```bash
./user_create.sh user1 user2 user3
```

---

# Interviewer May Ask: "Can you add sudo access?"

You can add:

```bash
usermod -aG wheel "$USERNAME"
```

On RHEL:

```text
wheel
```

On Ubuntu/Debian:

```text
sudo
```

For example:

```bash
usermod -aG wheel "$USERNAME"
```

Then verify:

```bash
id "$USERNAME"
```

---

# Interviewer May Ask: "How would you make it safer?"

Mention:

```text
1. Validate username
2. Check root privileges
3. Check whether user already exists
4. Don't hardcode passwords
5. Check exit status
6. Log operations
7. Use least privilege
8. Validate group before adding user
```

---

# Commands You Should Know for This Project

```bash
useradd
usermod
userdel
passwd
chage
groupadd
groupdel
getent
id
groups
```

### Most Important

```bash
useradd -m -s /bin/bash -g developers natraj

passwd natraj

usermod -aG wheel natraj

id natraj

chage -d 0 natraj
```

---

## Interview Difficulty

```text
Basic
  │
  ├── useradd
  ├── passwd
  └── id
  │
  ▼
Intermediate
  │
  ├── Arguments
  ├── if condition
  ├── Group creation
  └── Validation
  │
  ▼
Advanced ⭐
  │
  ├── Logging
  ├── Error handling
  ├── Multiple users
  ├── Password policy
  ├── Sudo/Wheel
  └── Input validation
```

