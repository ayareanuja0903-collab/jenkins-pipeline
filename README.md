# 🚀 Jenkins CI/CD Pipeline with Docker & Node.js

## 📌 Project Overview

This project implements an automated CI/CD pipeline using Jenkins to build and deploy a Dockerized Node.js application on AWS EC2. GitHub webhooks are used to trigger deployments on every code push.

---

## 🧰 Tech Stack

* Node.js
* Jenkins
* Docker
* PM2
* AWS EC2
* GitHub Webhooks

---

## 🏗️ Architecture

```
Developer → GitHub → Jenkins → Docker → AWS EC2 → End User
```

---

## ⚙️ Workflow

1. Code is pushed to GitHub
2. Webhook triggers Jenkins
3. Jenkins builds a Docker image
4. Existing container is replaced
5. Updated application is deployed on EC2

---

## ✨ Key Features

* Automated CI/CD pipeline
* Docker-based deployment
* Continuous deployment on code push
* Process management with PM2
* Container lifecycle handling

---

## ⚠️ Challenges

* Branch mismatch (`main` vs `master`)
* Webhook configuration issues
* Docker permission errors
* Port conflicts during deployment

---

## ✅ Solutions

* Set correct branch (`main`)
* Fixed webhook configuration
* Granted Docker access to Jenkins user
* Implemented container stop & remove logic

---

## 🎯 Outcome

* Automated build and deployment process
* Reduced manual effort and deployment errors
* Consistent application delivery using containers
* Live application deployed on AWS EC2

---

## 🌐 Access

```
http://<EC2-PUBLIC-IP>:3001
```

---

## 🔍 Verification

```bash
docker ps
docker logs node-container
```

---

## 📌 Conclusion

This project demonstrates a practical CI/CD pipeline using Jenkins and Docker, enabling efficient and reliable application deployment on AWS.
