# Advanced Gemini Clone - Enterprise DevSecOps Edition

![Gemini Clone Logo](public/assets/readme-banner.png)

A production-ready, highly optimized Google Gemini Clone built with Next.js, featuring a complete DevSecOps pipeline, Kubernetes orchestration, and GitOps deployment.

##  Project Overview

This project is an advanced recreation of the Gemini AI platform. It not only replicates the core functionalities of the original application but also introduces a robust, scalable, and secure infrastructure using modern DevOps practices.

### Key Highlights
- **Frontend & API:** Next.js 14, React 18, TailwindCSS, Zustand
- **AI Integration:** Google Generative AI API
- **Database:** MongoDB with Mongoose
- **Containerization:** Docker & Docker Compose
- **Orchestration:** Kubernetes (Kind)
- **CI/CD Pipeline:** Jenkins (Master/Agent architecture)
- **GitOps:** ArgoCD
- **Infrastructure as Code:** Terraform (AWS EC2)
- **Security & Quality:** SonarQube, Trivy, OWASP Dependency-Check
- **Observability:** Prometheus & Grafana

---

##  Architecture & Pipeline

Our DevSecOps pipeline ensures code quality, security, and seamless deployment:

1. **Continuous Integration (Jenkins):**
   - Source code checkout
   - Code Quality Analysis (SonarQube)
   - Software Composition Analysis (OWASP Dependency-Check)
   - Container Image Vulnerability Scanning (Trivy)
   - Docker Image Build & Push to Registry

2. **Continuous Deployment (ArgoCD):**
   - GitOps-based synchronization
   - Automated deployment to Kubernetes cluster
   - ConfigMap and Secret management

3. **Infrastructure (Terraform):**
   - Automated provisioning of AWS EC2 instances for Jenkins Master and Build Agents.

---

##  Getting Started

### 1. Local Development Setup

Clone the repository and install dependencies:

\\ash
git clone https://github.com/<YOUR_GITHUB_USERNAME>/dev-gemini-clone.git
cd dev-gemini-clone
npm install
\
Set up your environment variables (see \ENV_SETUP.md\ for details):
\\ash
cp .env.sample .env.local
# Add your Google OAuth, MongoDB URI, and NextAuth Secret
\
Run the development server:
\\ash
npm run dev
\
### 2. Docker Deployment

Build and run the application using Docker Compose:

\\ash
docker-compose up -d --build
\
### 3. Kubernetes Deployment (Kind & ArgoCD)

Provision a local Kubernetes cluster using Kind:
\\ash
kind create cluster --name gemini-cluster --config kind/kind-config.yml
\
Install ArgoCD and apply the application manifests:
\\ash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl apply -f kind/
\
---

##  Security & Code Quality

This project integrates industry-standard security tools:
- **SonarQube:** Enforces clean code standards and detects bugs/code smells.
- **Trivy:** Scans Docker images for OS packages and software dependencies vulnerabilities.
- **OWASP Dependency-Check:** Identifies project dependencies with known vulnerabilities.

---

##  Observability

Monitoring is configured using the Kube-Prometheus stack:
- **Prometheus:** Collects and stores metrics as time series data.
- **Grafana:** Visualizes metrics through comprehensive dashboards (Cluster health, API server status, Pod metrics).

---

##  License

This project is licensed under the MIT License.
