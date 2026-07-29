---
title: • multipal file
parent: • Linux
grand_parent: 11. Operating System (OS)
nav_order: 1.3
has_children: true
---

============================

```bash
mkdir -p docs/ansible
cd docs/ansible

topics=(
"Introduction"
"Installation"
"SSH Setup"
"Inventory"
"Ad-hoc Commands"
"Modules"
"YAML Basics"
"Playbooks"
"Variables"
"Conditionals & Loops"
"Handlers"
"Templates (Jinja2)"
"Roles"
"Ansible Vault"
"Collections"
"AWS Automation"
"Azure Automation"
"Docker & Kubernetes"
"Best Practices"
"Projects"
)

i=1

for topic in "${topics[@]}"; do
cat > "$i. $topic.md" <<EOF
---
title: "$i. $topic"
nav_order: $i
parent: "• Ansible"
grand_parent: "7. Configuration Management Tools"
has_children: true
---

# $i. $topic

EOF
((i++))
done

```

====================
If you're already inside the docs/ansible folder:

```bash
touch "1. Introduction.md" \
"2. Installation.md" \
"3. SSH Setup.md" \
"4. Inventory.md" \
"5. Ad-hoc Commands.md" \
"6. Modules.md" \
"7. YAML Basics.md" \
"8. Playbooks.md" \
"9. Variables.md" \
"10. Conditionals & Loops.md" \
"11. Handlers.md" \
"12. Templates (Jinja2).md" \
"13. Roles.md" \
"14. Ansible Vault.md" \
"15. Collections.md" \
"16. AWS Automation.md" \
"17. Azure Automation.md" \
"18. Docker & Kubernetes.md" \
"19. Best Practices.md" \
"20. Projects.md"
```

===================

Or create the folder and files in one go:

```bash
mkdir -p docs/ansible

cd docs/ansible

touch "1. Introduction.md" \
"2. Installation.md" \
"3. SSH Setup.md" \
"4. Inventory.md" \
"5. Ad-hoc Commands.md" \
"6. Modules.md" \
"7. YAML Basics.md" \
"8. Playbooks.md" \
"9. Variables.md" \
"10. Conditionals & Loops.md" \
"11. Handlers.md" \
"12. Templates (Jinja2).md" \
"13. Roles.md" \
"14. Ansible Vault.md" \
"15. Collections.md" \
"16. AWS Automation.md" \
"17. Azure Automation.md" \
"18. Docker & Kubernetes.md" \
"19. Best Practices.md" \
"20. Projects.md"

```
