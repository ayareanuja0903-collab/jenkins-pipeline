# 🚀 Jenkins CI/CD Pipeline with Docker & Node.js

This project demonstrates a complete **CI/CD pipeline** using Jenkins, Docker, and a Node.js application.

---

## 📌 Project Overview

This setup automates the process of:

* Pulling code from GitHub
* Building a Docker image
* Deploying the application in a container
* Running the application on an EC2 server

---

## 🛠️ Tech Stack

* Jenkins (CI/CD)
* Docker (Containerization)
* Node.js (Application)
* GitHub (Version Control)
* AWS EC2 (Deployment Server)

---

## 📂 Project Structure

```
.
├── Scrrenshots
├── Dockerfile
├── Jenkinsfile
├── app.js
├── package.json
└── README.md
```

---

## ⚙️ Setup Instructions

### 1️⃣ Launch EC2 Instance

* Create Ubuntu EC2 instance
* Open ports:

  * 22 (SSH)
  * 8080 (Jenkins)
  * 3001 (Application)

---

### 2️⃣ Install Dependencies

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk docker.io git npm
```

---

### 3️⃣ Start Services

```bash
sudo systemctl start docker
sudo systemctl enable docker

sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

### 4️⃣ Configure Jenkins

* Open Jenkins:

  ```
  http://<EC2-IP>:8080
  ```
* Install suggested plugins
* Create a pipeline job

---

### 5️⃣ Connect GitHub Repository

* Configure pipeline:

  * Pipeline script from SCM
  * SCM: Git
  * Repository URL:

    ```
    https://github.com/your-username/jenkins-pipeline.git
    ```
  * Branch: `main`
  * Script Path: `Jenkinsfile`

---

### 6️⃣ Setup GitHub Webhook

* Go to GitHub → Settings → Webhooks
* Add:

  ```
  http://<EC2-IP>:8080/github-webhook/
  ```
* Content type: `application/json`
* Event: Push

---

## 🐳 Dockerfile

```dockerfile
FROM node:18

WORKDIR /app

COPY package.json ./

RUN npm install

COPY . .

RUN npm install -g pm2

EXPOSE 3000

CMD ["pm2-runtime", "app.js"]
```

---

## ⚙️ Jenkinsfile

```groovy
pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker ps -q --filter "name=node-container" | grep -q . && docker stop node-container || true
                docker ps -aq --filter "name=node-container" | grep -q . && docker rm node-container || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3001:3000 --name node-container node-app'
            }
        }
    }
}
```

---

## 🚀 How It Works

1. Developer pushes code to GitHub
2. GitHub webhook triggers Jenkins
3. Jenkins pulls latest code
4. Docker image is built
5. Old container is removed
6. New container is deployed

---

## 🌐 Access Application

```
http://<EC2-IP>:3001
```

---

## 🔍 Verify Deployment

```bash
docker ps
```

---

## 🧹 Cleanup Commands

```bash
docker stop $(docker ps -q)
docker rm $(docker ps -aq)
docker image prune -f
```

## 👩‍💻 Author

Anuja Ayare

---

## ⭐ Acknowledgement

This project demonstrates a real-world DevOps CI/CD pipeline using Jenkins and Docker.
