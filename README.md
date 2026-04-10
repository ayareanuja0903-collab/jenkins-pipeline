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
├── Screenshots
├── Dockerfile
├── Jenkinsfile
├── app.js
├── package.json
└── README.md
```
✨ Key Features
````
Fully automated CI/CD pipeline
Dockerized Node.js application
Automated deployment on AWS EC2
Continuous deployment on every code push
Process management using PM2
Efficient container lifecycle management
````
⚠️ Challenges Faced
`````
Branch mismatch (master vs main)
GitHub webhook not triggering
Docker permission issues (/var/run/docker.sock)
Port conflicts during deployment

---
## ⚙️ CICD Workflow
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

## 🚀 How It Works

1. Developer pushes code to GitHub
2. GitHub webhook triggers Jenkins
3. Jenkins pulls latest code
4. Docker image is built
5. Old container is removed
6. New container is deployed

---
## 👩‍💻 Author

Anuja Ayare

---

## ⭐ Acknowledgement

This project demonstrates a real-world DevOps CI/CD pipeline using Jenkins and Docker.
