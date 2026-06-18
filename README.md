# 🚀 AWS EKS CI/CD Pipeline using Jenkins, Docker & Kubernetes

## 📌 Project Overview

This project demonstrates a complete DevOps CI/CD pipeline for deploying a Dockerized web application to an AWS Elastic Kubernetes Service (EKS) cluster using Jenkins.

The pipeline automates the complete deployment process, from source code management to container deployment on Kubernetes.

---

## 🏗️ Project Architecture

```
Developer
     │
     ▼
GitHub Repository
     │
 GitHub Webhook
     │
     ▼
 Jenkins Pipeline
     │
 ├── Clone Source Code
 ├── Build Docker Image
 ├── Push Image to Docker Hub
 ├── Configure AWS CLI
 ├── Connect to AWS EKS
 └── Deploy to Kubernetes
     │
     ▼
 Kubernetes Pods
     │
     ▼
 AWS Load Balancer
     │
     ▼
 Users
```

---

## 🛠️ Technologies Used

- Git
- GitHub
- Docker
- Docker Hub
- Jenkins
- AWS IAM
- AWS CLI
- Amazon EKS
- Kubernetes
- Apache Web Server
- Ubuntu Linux

---

## 📂 Project Structure

```
aws-eks-cicd-pipeline
│
├── Dockerfile
├── Jenkinsfile
├── README.md
│
├── k8s
│   ├── deployment.yml
│   └── service.yml
│
└── website
    ├── css
    ├── fonts
    ├── images
    ├── js
    ├── index.html
    └── ...
```

---

## ⚙️ CI/CD Pipeline Workflow

### 1. Developer pushes code to GitHub

The application source code is pushed to the GitHub repository.

↓

### 2. GitHub Webhook triggers Jenkins

Every push automatically starts the Jenkins pipeline.

↓

### 3. Jenkins clones the repository

Jenkins downloads the latest source code.

↓

### 4. Build Docker Image

The Dockerfile packages the website into a Docker image.

↓

### 5. Push Image to Docker Hub

The newly built Docker image is uploaded to Docker Hub.

↓

### 6. Configure AWS

Jenkins authenticates with AWS using IAM credentials.

↓

### 7. Connect to Amazon EKS

The pipeline updates the Kubernetes configuration.

↓

### 8. Deploy to Kubernetes

Deployment and Service YAML files are applied to the EKS cluster.

↓

### 9. Application becomes available

The website is exposed through an AWS Load Balancer.

---

## 📦 Docker

The application is containerized using Docker.

The Dockerfile:

- Uses Ubuntu as the base image
- Installs Apache Web Server
- Copies website files
- Starts Apache

---

## ☸️ Kubernetes

### Deployment

- Creates application Pods
- Maintains desired replicas
- Supports rolling updates
- Self-healing

### Service

- Type: LoadBalancer
- Exposes the application
- Routes traffic to Pods

---

## 🔄 Jenkins Pipeline Stages

- Clone Source Code
- Build Docker Image
- Push Docker Image
- Configure AWS
- Connect to EKS
- Deploy Application

---

## 🎯 Features

- Automated CI/CD Pipeline
- Dockerized Application
- Kubernetes Deployment
- AWS EKS Integration
- GitHub Webhook Integration
- Jenkins Pipeline Automation
- Load Balancer Deployment

---

## 📚 Learning Outcomes

Through this project, I learned:

- Git and GitHub workflow
- Docker image creation
- Docker Hub integration
- Jenkins Pipeline automation
- AWS CLI configuration
- Amazon EKS deployment
- Kubernetes Deployment and Service configuration
- Continuous Integration and Continuous Deployment (CI/CD)

---

## 👩‍💻 Author

**Mayuri Bhosale**

GitHub: https://github.com/mayuri1203bhosale