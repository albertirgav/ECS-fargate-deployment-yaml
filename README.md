# Deployment YAML for ECS Fargate Application 🚀

This repository contains a containerized **frontend + backend** application deployed on **AWS ECS Fargate** using a **GitHub Actions CI/CD pipeline**.

This repository is designed with **production-ready DevOps practices**:

* Single ECR repository
* Separate frontend & backend services
* Automated build & deploy on every `main` branch push

---

## 🏗️ Architecture Overview

* **AWS ECS (Fargate)** – container orchestration
* **Amazon ECR** – Docker image registry (single repo)
* **GitHub Actions** – CI/CD pipeline
* **Docker** – containerization

```
GitHub Push (main)
        ↓
GitHub Actions
        ↓
Docker Build (FE + BE)
        ↓
Amazon ECR
        ↓
AWS ECS Fargate
```

---

## 📁 Project Structure

```
project-root/
├── .github/workflows/
│   └── deploy.yml
├── frontend/
│   └── Dockerfile
├── backend/
│   └── Dockerfile
└── README.md
```

---

## 🔁 CI/CD Pipeline Behavior

The pipeline is triggered when code is pushed to the **main** branch.

### Pipeline Steps

1. Checkout repository
2. Authenticate to AWS
3. Login to Amazon ECR
4. Build & push **backend** Docker image
5. Build & push **frontend** Docker image
6. Force new deployment for ECS services

> ECS pulls the latest image tags and redeploys containers automatically.

---

## 🐳 Docker Images

Both services use the **same ECR repository** with different tags:

| Service  | Image Tag   |
| -------- | ----------- |
| Backend  | `:backend`  |
| Frontend | `:frontend` |

---

## 🔐 GitHub Secrets Configuration

The following secrets **must be configured** in the GitHub repository:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```

The IAM user should have at least:

* `AmazonECRFullAccess`
* `AmazonECSFullAccess`

---

## ☁️ AWS Resources Used

* ECS Cluster (Fargate)
* ECS Services

  * Frontend Service
  * Backend Service
* ECS Task Definitions
* Amazon ECR Repository

---

## 🚀 Deployment

Deployment is fully automated.

Simply push to `main`:

```bash
git push origin main
```

GitHub Actions will handle the rest.

---

## 🧩 Future Improvements

* Task Definition auto revision update
* Environment separation (staging / production)
* Commit SHA based image tagging
* ALB health check validation
* Rollback strategy
* AWS Secrets Manager integration
