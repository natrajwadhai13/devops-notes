---
title: • Jenkins
parent: 2. CICD Tools
nav_order: 3
has_children: true
---


---

## ✅ Sample `Jenkinsfile` (Declarative Pipeline)

```groovy
pipeline {
    agent any

    environment {
        REGISTRY = "docker.io/natrajwadhai"   // Replace with your Docker Hub or private registry
        IMAGE_NAME = "myapp"
        TAG = "${env.BUILD_NUMBER}"
    }

    options {
        timestamps()
        ansiColor('xterm')
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-repo/app.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo "🛠️ Building the application..."
                sh 'docker build -t $REGISTRY/$IMAGE_NAME:$TAG .'
            }
        }

        stage('Test') {
            steps {
                echo "✅ Running unit tests..."
                sh './scripts/run_tests.sh'  // Or npm test / mvn test etc.
            }
        }

        stage('Push to Registry') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $REGISTRY/$IMAGE_NAME:$TAG
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying to server..."
                sh 'ansible-playbook deploy.yml -i inventory/production.ini'
            }
        }
    }

    post {
        success {
            echo "✅ Build #${env.BUILD_NUMBER} completed successfully!"
        }
        failure {
            echo "❌ Build failed. Check console logs."
        }
    }
}
```

---

## 🧰 Key Components

| Section            | Purpose                               |
| ------------------ | ------------------------------------- |
| `agent any`        | Run on any available Jenkins node     |
| `environment`      | Define reusable environment variables |
| `git`              | Pull code from GitHub                 |
| `docker build`     | Build Docker image                    |
| `docker push`      | Push to Docker Hub                    |
| `ansible-playbook` | Trigger deployment                    |
| `post`             | Success/failure notification block    |

---

## 🧪 Required Jenkins Setup

* **Docker** installed on the Jenkins agent
* **Git** access to your repo
* **Credentials** ID `docker-hub-creds` with Docker Hub username/password
* Optional: **Ansible** installed to run playbooks
* `scripts/run_tests.sh` or equivalent should exist

---

## 🔧 Customize For You


* A Jenkinsfile with **multi-branch support**?
* A **Node.js, Java, or Python-specific pipeline**?
* Deployment to **AWS EC2 / EKS / Lambda** or **Azure**?


======================================

Need Reaarange


## 🔹 **Jenkins – Answers**

**Q1. What is Jenkins and why is it used in DevOps?**

👉 Jenkins is an open-source automation server used for CI/CD. It automates building, testing, and deploying applications, helping DevOps teams deliver faster with fewer errors.

---

**Q2. What is the difference between freestyle jobs and pipeline jobs in Jenkins?**

👉
* **Freestyle job** → Simple, GUI-based, limited flexibility.
* **Pipeline job** → Uses Groovy-based Jenkinsfile, supports complex workflows, version-controlled pipelines.

---

**Q3. How does Jenkins integrate with GitHub/GitLab for continuous integration?**

👉 Jenkins integrates via **webhooks and plugins**.

* Webhook notifies Jenkins when code is pushed.
* Jenkins pulls code, runs build/test jobs, and reports results back to GitHub/GitLab.

---

**Q4. What are Jenkins plugins, and can you give 2–3 commonly used plugins?**

👉 Plugins extend Jenkins functionality. Some common ones are:

* **Git plugin** → integrates with Git.
* **Pipeline plugin** → supports Jenkinsfile-based pipelines.
* **Email Extension plugin** → sends build status notifications.

---

**Q5. Explain the difference between declarative pipeline and scripted pipeline in Jenkins.**

👉
* **Declarative pipeline** → Simple, YAML-like syntax, easier for beginners, structured stages/steps.
* **Scripted pipeline** → Written in Groovy, more flexible but complex, used for advanced scenarios.

---
