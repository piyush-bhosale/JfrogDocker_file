# 🐳 JFrog Artifactory OSS – Multi-Stage Docker Image

## 📘 Overview

This project provides a **multi-stage Dockerfile** for building a hardened, production-ready image of **JFrog Artifactory OSS**.  
It uses a custom **Ubuntu base layer** to pre-install dependencies and create required directory structure before layering on the official JFrog Artifactory image.

---

## ⚙️ What This Dockerfile Does

### 🧱 Stage 1: Base (Ubuntu 22.04)
- Installs essential dependencies:
  - `openjdk-17-jdk`, `curl`, `wget`, etc.
- Creates JFrog directory structure:
  ```
  /jfrog/artifactory/var/etc
  /jfrog/artifactory/var/log
  /jfrog/artifactory/var/data
  ```

### 📦 Stage 2: JFrog Artifactory OSS
- Pulls the latest `jfrog/artifactory-oss` image from JFrog’s official Docker registry
- Copies dependencies and folder structure from the base image
- Keeps default entrypoint and behavior

---

## 📁 Files Included

| File                        | Description |
|-----------------------------|-------------|
| `Dockerfile.jfrog-multistage` | Multi-stage Dockerfile for JFrog Artifactory |
| `README.md`                 | This documentation file |

---

## 🚀 Build & Push to AWS ECR

### 🧪 1. Build Docker Image
```bash
docker build -t jfrog-artifactory:custom -f Dockerfile.jfrog-multistage .
```

### 🏷️ 2. Tag for AWS ECR
```bash
docker tag jfrog-artifactory:custom <aws_account_id>.dkr.ecr.<region>.amazonaws.com/jfrog-artifactory:latest
```

### 🔐 3. Authenticate with ECR
```bash
aws ecr get-login-password --region <region> | \
docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
```

### ☁️ 4. Push Image to ECR
```bash
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/jfrog-artifactory:latest
```

---

## 🌐 Run Locally (Optional)

To test the image on your local system:
```bash
docker run -d -p 8082:8082 jfrog-artifactory:custom
```
Access Artifactory in your browser at:  
➡️ `http://localhost:8082`

---

## ✅ Highlights

- 🔒 Multi-stage hardened Docker image
- 🛠️ Ubuntu-based dependency layer
- 🐳 Pulls latest official JFrog OSS image
- ☁️ Compatible with AWS ECR, Jenkins, and Kubernetes
- 📦 Lightweight and clean image with reusable structure

---

## 👨‍💻 Author

**Piyush Bhosale**  
DevOps Engineer | Docker | AWS | Jenkins | JFrog | CI/CD | Kubernetes  
🔗 [GitHub Profile](https://github.com/piyush-bhosale)

---

## ⭐ Why This Repo Matters

- Demonstrates Docker multi-stage builds  
- Shows real-world use of JFrog Artifactory OSS  
- Deployable in cloud, CI/CD, or local environments  
- Clean, documented, and **recruiter-ready**
