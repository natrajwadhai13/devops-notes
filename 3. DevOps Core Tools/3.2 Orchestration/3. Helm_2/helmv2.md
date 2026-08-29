---
title: "• Helmv3"
parent: 3. DevOps Core Tools
nav_order: 3
has_children: true
---

# Helm – Short, Practical & Interview-Ready Notes

## 1. What is Helm?

**Helm is the package manager for Kubernetes.**

It packages Kubernetes manifests into reusable **Helm Charts** and makes application deployment easier through:

- Reusable templates
- Configuration through `values.yaml`
- Versioned releases
- Easy install, upgrade and rollback
- Environment-specific configuration
- CI/CD and GitOps integration

### Why Helm?

Without Helm, Kubernetes YAML files can become repetitive and difficult to manage across environments such as dev, stage and prod.

**Simple interview answer:**

> Helm is a package manager for Kubernetes. It uses reusable charts and templates to simplify application deployment, configuration, upgrades and rollbacks.

---

## 2. Important Helm Terminology

| Term            | Meaning                                                       |
| --------------- | ------------------------------------------------------------- |
| **Chart**       | A Helm package containing templates, values and metadata      |
| **Release**     | A running/installed instance of a chart                       |
| **Repository**  | A location from which Helm charts can be stored and retrieved |
| **values.yaml** | Default configuration values used by chart templates          |
| **templates/**  | Kubernetes manifest templates                                 |
| **Chart.yaml**  | Chart metadata such as name and version                       |

### Easy way to remember

**Chart = Package**  
**Release = Installed Package**  
**values.yaml = Configuration**  
**templates = Kubernetes YAML Templates**

---

## 3. Helm Architecture

### Helm 3

```text
Helm CLI
   |
   | Chart + Values
   v
Template Rendering
   |
   | Final Kubernetes Manifests
   v
Kubernetes API Server
   |
   v
Kubernetes Resources
(Pods, Deployments, Services, Ingress, HPA...)
```

### How Helm works

1. User runs a Helm command.
2. Helm reads the chart.
3. Helm loads `values.yaml` and any overrides.
4. Helm renders the templates into Kubernetes manifests.
5. Helm sends the resulting manifests to the Kubernetes API server.
6. Kubernetes creates or updates the resources.
7. Helm tracks the release and its revisions.

**Important:** Helm 3 does not use Tiller. Tiller was removed from Helm 3.

---

# 4. Helm Chart Structure

Create a chart:

```bash
helm create apache-helm
```

Typical structure:

```text
apache-helm/
├── Chart.yaml
├── values.yaml
├── charts/
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    ├── hpa.yaml
    ├── serviceaccount.yaml
    ├── _helpers.tpl
    ├── NOTES.txt
    └── tests/
        └── test-connection.yaml
```

### Main files

#### Chart.yaml

Contains chart metadata:

- Name
- Chart version
- App version
- Description
- Kubernetes version requirements, when configured

#### values.yaml

Contains default configurable values such as:

```yaml
replicaCount: 2

image:
  repository: nginx
  tag: "latest"

service:
  type: ClusterIP
  port: 80
```

#### templates/

Contains Kubernetes manifests with Helm variables.

Example:

```yaml
image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
```

The values come from `values.yaml` or another values source.

---

# 5. Install Helm

Example installation:

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4
chmod 700 get_helm.sh
./get_helm.sh
```

Verify:

```bash
helm version
```

---

# 6. Basic Helm Commands

## Create a Chart

```bash
helm create apache-helm
```

## Install a Chart

```bash
helm install dev-apache ./apache-helm
```

With namespace:

```bash
helm install dev-apache ./apache-helm \
  -n dev --create-namespace
```

## List Releases

```bash
helm list
```

Specific namespace:

```bash
helm list -n dev
```

## Upgrade a Release

```bash
helm upgrade dev-apache ./apache-helm -n dev
```

## Uninstall a Release

```bash
helm uninstall dev-apache -n dev
```

## Check Release History

```bash
helm history dev-apache -n dev
```

## Rollback

```bash
helm rollback dev-apache 1 -n dev
```

**Remember:** The number is the revision to which you want to roll back.

---

# 7. Validate and Preview a Chart

## Lint

Checks the chart for common problems:

```bash
helm lint ./apache-helm
```

## Render Templates Locally

Shows the Kubernetes YAML that Helm would generate:

```bash
helm template dev-apache ./apache-helm
```

## Dry Run + Debug

Useful before deployment:

```bash
helm install dev-apache ./apache-helm \
  --dry-run --debug
```

### Quick difference

```text
helm lint
    ↓
Check chart structure/problems

helm template
    ↓
See rendered Kubernetes YAML

helm install --dry-run --debug
    ↓
Preview installation without actually installing
```

---

# 8. Override values.yaml

You do not need to edit `values.yaml` for every environment.

## Using --set

```bash
helm install myapp ./apache-helm \
  --set replicaCount=5
```

## Using a custom values file

Example:

```text
values.yaml
values-dev.yaml
values-prod.yaml
```

Install with production values:

```bash
helm install prod-apache ./apache-helm \
  -f values-prod.yaml \
  -n prod --create-namespace
```

### Example

`values-dev.yaml`:

```yaml
replicaCount: 1

image:
  tag: "dev"
```

`values-prod.yaml`:

```yaml
replicaCount: 4

image:
  tag: "stable"

autoscaling:
  enabled: true
  minReplicas: 4
  maxReplicas: 10
  targetCPUUtilizationPercentage: 60
```

**Interview point:**

> `values.yaml` provides default values, while environment-specific files override those defaults.

---

# 9. Helm Repository and OCI Charts

## Search configured repositories

```bash
helm search repo nginx
helm search repo argocd
```

## List repositories

```bash
helm repo list
```

Online chart discovery can be done through Artifact Hub.

Helm also supports charts stored in OCI registries.

Example:

```bash
helm install nginx-helm \
  oci://registry-1.docker.io/bitnamicharts/nginx
```

With namespace:

```bash
helm install nginx-helm \
  oci://registry-1.docker.io/bitnamicharts/nginx \
  -n nginx --create-namespace
```

---

# 10. Helm Chart Dependencies

A chart can depend on other charts.

Example in `Chart.yaml`:

```yaml
dependencies:
  - name: redis
    version: 17.3.0
    repository: "https://charts.bitnami.com/bitnami"
```

Update/download dependencies:

```bash
helm dependency update
```

**Example use case:**

An application chart may depend on Redis or another supporting service.

---

# 11. Helm Lifecycle

The most important lifecycle commands are:

```text
Create
  ↓
helm create

Validate
  ↓
helm lint

Preview
  ↓
helm template / --dry-run

Install
  ↓
helm install

Upgrade
  ↓
helm upgrade

Check history
  ↓
helm history

Rollback
  ↓
helm rollback

Remove
  ↓
helm uninstall
```

---

# 12. Helm + GitOps

Helm is commonly used with GitOps tools such as **Argo CD** and **Flux**.

Typical flow:

```text
Developer
   |
   v
Git Repository
   |
   v
Argo CD
   |
   v
Helm Chart
   |
   v
Kubernetes Cluster
```

Typical environment structure:

```text
myapp/
├── Chart.yaml
├── values.yaml
├── values-dev.yaml
├── values-stage.yaml
├── values-prod.yaml
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    └── hpa.yaml
```

### Why Helm is useful with GitOps

- Charts and configuration can be stored in Git.
- Environments can use different values files.
- Deployments become repeatable.
- Changes can be reviewed through Git.
- Rollbacks can be performed through Helm or Git-based workflows.

---

# 13. Helm vs Kubernetes YAML

| Kubernetes YAML                        | Helm                                |
| -------------------------------------- | ----------------------------------- |
| Static manifests                       | Templates                           |
| More repetition                        | Reusable charts                     |
| Manual configuration changes           | Values-based configuration          |
| Difficult to reuse across environments | Easy environment-specific overrides |
| No Helm release history                | Release revisions and rollback      |
| Applied with `kubectl`                 | Managed with Helm                   |

**Interview answer:**

> Kubernetes manifests define resources directly. Helm packages those manifests into reusable charts and adds templating, configuration management, release history, upgrades and rollbacks.

---

# 14. Helm vs Kustomize

| Feature            | Helm                            | Kustomize                                      |
| ------------------ | ------------------------------- | ---------------------------------------------- |
| Main purpose       | Package and deploy applications | Customize Kubernetes YAML                      |
| Templating         | Yes                             | No traditional templating                      |
| Main configuration | `values.yaml`                   | `kustomization.yaml`                           |
| Packaging          | Yes                             | No                                             |
| Release management | Yes                             | No Helm-style releases                         |
| Rollback           | Helm revision support           | Usually handled through Git/deployment tooling |

**Easy interview answer:**

> Helm is mainly for packaging, templating and release management. Kustomize is mainly for customizing existing Kubernetes YAML without templates.

---

# 15. Practical Hands-on: Apache with Helm

## Step 1: Create chart

```bash
helm create apache-helm
```

## Step 2: Configure values

Example:

```yaml
image:
  repository: httpd
  tag: latest
  pullPolicy: IfNotPresent

replicaCount: 2
```

Enable ingress/HPA in the chart values when those resources are configured in the templates.

## Step 3: Validate

```bash
helm lint apache-helm
helm template apache-helm
```

## Step 4: Install

```bash
helm install dev-apache apache-helm \
  -n dev --create-namespace
```

## Step 5: Check resources

```bash
kubectl get all -n dev
```

## Step 6: Upgrade

After changing chart configuration:

```bash
helm upgrade dev-apache apache-helm -n dev
```

## Step 7: Check history

```bash
helm history dev-apache -n dev
```

## Step 8: Rollback

```bash
helm rollback dev-apache 1 -n dev
```

## Step 9: Remove

```bash
helm uninstall dev-apache -n dev
```

---

# 16. Important Helm Interview Questions

### Q1. What is Helm?

Helm is a package manager for Kubernetes. It uses reusable charts and templates to simplify application deployment and configuration.

### Q2. What is a Helm Chart?

A Helm Chart is a package containing Kubernetes templates, default values and chart metadata.

### Q3. What is a Helm Release?

A release is an installed instance of a Helm chart.

Example:

```text
Chart: apache-helm
Release: dev-apache
```

### Q4. What is values.yaml?

It contains default configuration values used by Helm templates.

### Q5. Difference between Chart.yaml and values.yaml?

```text
Chart.yaml  → Chart metadata
values.yaml → Application configuration
```

### Q6. How do you override values?

```bash
helm install myapp ./chart --set replicaCount=5
```

or:

```bash
helm install myapp ./chart -f values-prod.yaml
```

### Q7. How do you upgrade a Helm release?

```bash
helm upgrade myapp ./chart
```

### Q8. How do you rollback?

```bash
helm history myapp
helm rollback myapp 1
```

### Q9. How do you debug a Helm chart?

```bash
helm lint ./chart
helm template ./chart
helm install myapp ./chart --dry-run --debug
helm get manifest myapp
helm get values myapp
helm history myapp
```

### Q10. What happened to Tiller?

Tiller was used by Helm 2. It was removed in Helm 3. Helm 3 works directly with the Kubernetes API.

### Q11. Can Helm work with Argo CD?

Yes. Argo CD can use Helm charts as an application deployment method in a GitOps workflow.

### Q12. What are Helm Hooks?

Hooks are special Helm resources/templates that can run at specific points in a release lifecycle.

Common use cases include:

- Database migrations
- Pre/post deployment tasks
- Cleanup jobs

---

# 17. Most Important Commands – Quick Cheat Sheet

```bash
# Create
helm create mychart

# Validate
helm lint ./mychart

# Preview
helm template myapp ./mychart

# Install
helm install myapp ./mychart

# Install with namespace
helm install myapp ./mychart -n dev --create-namespace

# Install with values
helm install myapp ./mychart -f values-prod.yaml

# Override a value
helm install myapp ./mychart --set replicaCount=3

# List releases
helm list -n dev

# Upgrade
helm upgrade myapp ./mychart -n dev

# History
helm history myapp -n dev

# Rollback
helm rollback myapp 1 -n dev

# Get rendered manifest
helm get manifest myapp -n dev

# Get release values
helm get values myapp -n dev

# Uninstall
helm uninstall myapp -n dev

# Package
helm package ./mychart

# Dependencies
helm dependency update
```

---

# 18. Interview Revision – Remember These 10 Points

1. **Helm = Kubernetes package manager**
2. **Chart = package**
3. **Release = installed chart**
4. **Chart.yaml = metadata**
5. **values.yaml = configuration**
6. **templates/ = Kubernetes manifests with variables**
7. **`helm install` = deploy**
8. **`helm upgrade` = update**
9. **`helm rollback` = previous revision**
10. **Helm 3 = no Tiller**

### One-line interview summary

> Helm is a Kubernetes package manager that uses reusable charts, templates and values to standardize deployments and provides release management such as install, upgrade and rollback.
