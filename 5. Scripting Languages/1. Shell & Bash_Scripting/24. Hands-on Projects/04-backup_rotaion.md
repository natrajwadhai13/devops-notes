---
title: "1. backup_rotaion"
nav_order: 4
parent: "24. Hands-on Projects"
grand_parent: "• Shell & Bash_Scripting"
grand_grand_parent: "5. Scripting Languages"
---

```bash

#!/bin/bash

#######################################################
# Script Name : backup.sh
# Author      : Natraj
# Description : Backup files/folders with timestamp
#               Keep only latest 5 backups
#######################################################

############ Variables #################

SOURCE="/home/user/Documents"
BACKUP_DIR="/home/user/Backup"

DATE=$(date +"%Y-%m-%d_%H-%M-%S")

BACKUP_NAME="backup_$DATE"

LOGFILE="$BACKUP_DIR/backup.log"

MAX_BACKUP=5

########################################


############ Function ##################

log_message() {
    echo "$(date +"%Y-%m-%d %H:%M:%S") : $1" | tee -a "$LOGFILE"
}

########################################


############ Check Source ##############

check_source() {

    if [ ! -d "$SOURCE" ]; then
        log_message "ERROR : Source directory does not exist."
        exit 1
    fi

}

########################################


############ Create Backup Directory ####

create_backup_dir() {

    if [ ! -d "$BACKUP_DIR" ]; then
        mkdir -p "$BACKUP_DIR"

        if [ $? -ne 0 ]; then
            log_message "ERROR : Unable to create Backup Directory."
            exit 1
        fi
    fi

}

########################################


############ Backup Function ###########

take_backup() {

    cp -r "$SOURCE" "$BACKUP_DIR/$BACKUP_NAME"

    if [ $? -eq 0 ]; then
        log_message "Backup Created Successfully : $BACKUP_NAME"
    else
        log_message "ERROR : Backup Failed."
        exit 1
    fi

}

########################################


########### Delete Old Backup ##########

delete_old_backup() {

    BACKUP_COUNT=$(ls -1dt "$BACKUP_DIR"/backup_* 2>/dev/null | wc -l)

    if [ "$BACKUP_COUNT" -gt "$MAX_BACKUP" ]; then

        ls -1dt "$BACKUP_DIR"/backup_* | tail -n +6 | while read OLD_BACKUP
        do
            rm -rf "$OLD_BACKUP"

            if [ $? -eq 0 ]; then
                log_message "Deleted Old Backup : $(basename "$OLD_BACKUP")"
            else
                log_message "ERROR : Unable to delete $(basename "$OLD_BACKUP")"
            fi
        done

    fi

}

########################################


############ Main ######################

log_message "========== Backup Started =========="

check_source

create_backup_dir

take_backup

delete_old_backup

log_message "========== Backup Completed =========="

########################################


```

```bash

#!/bin/bash

<< readme
This is a backup script for 5 day rotation.
It will create a backup of the specified source directory and store it in the backup directory with a timestamp. The script will keep only the latest 5 backups and delete older ones.

Useage:
./backup.sh <path to your source> <path to your backup directory>
./backup1.sh /root/Documents /root   --- this is example of how to run the script

readme

function display_usage {
    echo "Usage: ./backup.sh <path of your source> <path to your backup directory>"
}

if [ $# -eq 0 ]; then
    display_usage
fi

source_dir=$1
timestamp=$(date +%Y%m%d_%H%M%S)
backup_dir=$2

function create_backup {
    zip -r "$backup_dir/backup_$timestamp.zip" "$source_dir" > /dev/null

    if [ $? -eq 0 ]; then
        echo "Backups generated successfully for $timestamp.zip"
    else
        echo "Backup failed!"
        exit 1
    fi
}

function perfom_rotation {

    backups=($(ls -t "$backup_dir"/backup_*.zip 2>/dev/null))

    if [ "${#backups[@]}" -gt 5 ]; then
        echo "Performing rotation for 5 days"

        backups_to_remove=("${backups[@]:5}")

        for backup in "${backups_to_remove[@]}"; do
            rm -f "$backup"
        done
    fi
}

create_backup
perfom_rotation

```

explain it line by line in simple language. Most beginners get confused by `$`, `{}`, `()`, `[]`, and `[@]`. Once you understand these, Bash becomes much easier.

---

# 1. User passes arguments

Command:

```bash
bash backup1.sh /root/Documents /root/
```

Bash stores the arguments like this:

| Variable | Value                   |
| -------- | ----------------------- |
| `$0`     | backup1.sh              |
| `$1`     | /root/Documents         |
| `$2`     | /root/                  |
| `$#`     | 2 (number of arguments) |

So,

```bash
source_dir=$1
```

becomes

```bash
source_dir=/root/Documents
```

and

```bash
backup_dir=$2
```

becomes

```bash
backup_dir=/root/
```

---

# 2. `$#`

```bash
if [ $# -eq 0 ]; then
```

`$#` means:

> "How many arguments did the user pass?"

Examples:

```
bash backup.sh
```

```
$# = 0
```

```
bash backup.sh /root/Documents
```

```
$# = 1
```

```
bash backup.sh /root/Documents /root/
```

```
$# = 2
```

So

```bash
if [ $# -eq 0 ]
```

means

> If user didn't give any argument.

---

# 3. Timestamp

```bash
timestamp=$(date +%Y%m%d_%H%M%S)
```

This executes:

```bash
date +%Y%m%d_%H%M%S
```

Example output

```
20260725_150100
```

and stores it inside

```
timestamp
```

So later

```bash
backup_$timestamp.zip
```

becomes

```
backup_20260725_150100.zip
```

---

# 4. `$( )`

This is called **Command Substitution**.

```
$(command)
```

means

> Run the command and store its output.

Example

```bash
today=$(date)
```

becomes

```
today="Fri Jul 25"
```

Another example

```bash
hostname=$(hostname)
```

becomes

```
hostname=k8s-master
```

---

# 5. This line

```bash
zip -r "$backup_dir/backup_$timestamp.zip" "$source_dir"
```

Suppose

```
backup_dir=/root
timestamp=20260725_150100
source_dir=/root/Documents
```

Bash actually runs

```bash
zip -r /root/backup_20260725_150100.zip /root/Documents
```

---

# 6. `$?`

Immediately after every command,

```
$?
```

contains its exit status.

Example

```
zip ....
```

Success

```
$? = 0
```

Failure

```
$? = 1
```

or

```
2
```

etc.

Therefore

```bash
if [ $? -eq 0 ]
```

means

> Did zip command succeed?

---

# 7. Array

This line is the most confusing.

```bash
backups=($(ls -t "$backup_dir"/backup_*.zip))
```

Let's simplify.

Suppose

```
ls -t
```

returns

```
backup7.zip
backup6.zip
backup5.zip
backup4.zip
backup3.zip
backup2.zip
backup1.zip
```

Then

```
backups
```

becomes

```
Index      Value

0          backup7.zip
1          backup6.zip
2          backup5.zip
3          backup4.zip
4          backup3.zip
5          backup2.zip
6          backup1.zip
```

---

# 8. `${#backups[@]}`

Very important.

```
backups[@]
```

means

> All elements of array.

```
#backups
```

means

> Count

Therefore

```bash
${#backups[@]}
```

means

> Total number of backups.

Example

```
backup7
backup6
backup5
backup4
backup3
backup2
backup1
```

Count

```
7
```

So

```bash
if [ "${#backups[@]}" -gt 5 ]
```

means

```
If total backups are greater than 5
```

---

# 9. Slice

This line

```bash
backups_to_remove=("${backups[@]:5}")
```

looks difficult but is very simple.

Suppose

```
Index

0 backup7
1 backup6
2 backup5
3 backup4
4 backup3
5 backup2
6 backup1
```

```
:5
```

means

> Start from index **5**

So

```
backups_to_remove
```

becomes

```
backup2
backup1
```

The newest 5 are kept.

Everything after index 5 will be deleted.

---

# 10. Loop

```bash
for backup in "${backups_to_remove[@]}"
```

means

Take one backup at a time.

Iteration 1

```
backup=backup2.zip
```

Iteration 2

```
backup=backup1.zip
```

Then

```bash
rm -f "$backup"
```

becomes

```
rm -f backup2.zip
```

then

```
rm -f backup1.zip
```

---

# 11. Why quotes?

Example

```
backup="/root/My Folder/file.zip"
```

Without quotes

```bash
rm $backup
```

becomes

```
rm /root/My Folder/file.zip
```

Bash thinks

```
My
```

and

```
Folder
```

are separate arguments.

With quotes

```bash
rm "$backup"
```

it becomes

```
rm "/root/My Folder/file.zip"
```

Always use quotes around variables that represent filenames or paths.

---

# 12. `${}`

You asked about braces.

Simple variable

```bash
$backup
```

works.

But when attaching text,

```bash
backup=file

echo "${backup}.zip"
```

becomes

```
file.zip
```

Without braces, Bash can get confused about where the variable name ends.

---

# Easy rule to remember

| Symbol            | Meaning                                                    |
| ----------------- | ---------------------------------------------------------- |
| `$1`              | First argument                                             |
| `$2`              | Second argument                                            |
| `$#`              | Number of arguments                                        |
| `$?`              | Previous command status                                    |
| `$(command)`      | Execute a command and capture its output                   |
| `()`              | Create an array or run a command substitution (with `$()`) |
| `[]`              | Test/condition (`if`, `while`)                             |
| `${var}`          | Variable expansion                                         |
| `${#array[@]}`    | Number of elements in an array                             |
| `"${array[@]:5}"` | Array slice starting from index 5                          |
| `[@]`             | All elements of an array                                   |

---
