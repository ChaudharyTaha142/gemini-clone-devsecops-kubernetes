# Gemini Clone – Production-Ready DevSecOps Deployment with Kubernetes, Jenkins, and GitOps

![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestrated-blue)
![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-red)
![DevSecOps](https://img.shields.io/badge/DevSecOps-Production-green)
![GitOps](https://img.shields.io/badge/GitOps-Enabled-orange)

A production-grade AI chat application inspired by Google Gemini, built using **Next.js 14**, **Google Generative AI**, **MongoDB**, and **NextAuth**, and fully deployed using modern **DevSecOps** practices including Docker containerization, Kubernetes orchestration, Jenkins CI/CD automation, and GitOps-based continuous deployment.

This project demonstrates a complete DevOps lifecycle implementation from infrastructure provisioning to automated deployment in a Kubernetes environment.

---

## 🚀 DevOps Architecture Overview

**Flow:** Development → Docker → Jenkins CI/CD → Docker Registry → Kubernetes Deployment → Ingress Routing → Production

Key DevOps capabilities implemented:

- Containerization using Docker with production-ready builds
- Kubernetes orchestration with Deployments, Services, Ingress, HPA, ConfigMaps, and Secrets
- CI/CD automation using Jenkins pipelines (Kubernetes-based Jenkins setup)
- GitOps-compatible deployment workflow using declarative Kubernetes manifests
- Secure secrets and configuration management (ConfigMap + Secret split)
- Persistent storage using Kubernetes Persistent Volumes and PVCs
- Reverse proxy and SSL using Nginx Ingress + cert-manager (Let’s Encrypt)

---
## 🏗️ DevOps Architecture Diagram

This project follows a production-grade DevSecOps workflow:

```
Developer → GitHub → Jenkins CI/CD → Docker Image Build → Container Registry → Kubernetes Deployment → Ingress Controller → End Users
```

**Components involved:**


- **Jenkins** → CI/CD automation
- **Docker** → Application containerization
- **Kubernetes** → Orchestration and scaling
- **Nginx Ingress** → Traffic routing
- **cert-manager** → TLS automation
- **MongoDB** → Persistent storage

---
## ✨ Application Features

This project is also a feature-rich clone of Google Gemini with:

- Fast, optimized responses using the **@google/generative-ai** SDK
- Modern, responsive UI with custom components, micro-animations, and theming
- Persistent, authenticated chat experience with MongoDB + NextAuth
- End-to-end production deployment using Docker, Kubernetes, and Jenkins pipelines

If you’re looking for a real-world, end-to-end **AI app + DevSecOps** reference project, this repo is built for exactly that.

---

## 💬 Core Chat Features

### Chat & AI
- Interactive AI chat powered by **Google Generative AI**
- Support for **editing prompts** and regenerating responses
- **Chat management**: create, rename, delete, pin previous conversations
- **Optimistic UI** and loaders for smooth UX
- **Prompt Gallery** with curated prompts and masonry layout
- **Code-aware responses** with syntax highlighting

### Rich UX
- Fully responsive layout (desktop + mobile)
- **Dark / Light mode** via `next-themes`
- **Framer Motion** micro-animations
- Custom `dev-components` (buttons, modals, drawers, toggles, tooltips, toasts)
- Text input helpers: random prompts, actions, shortcuts

### Media & Accessibility
- **Text-to-Speech** and **Speech-to-Text** integrations
- Share chat links and copy-to-clipboard
- Image-friendly chat experience (with mobile support)
### Auth & State
- Authentication with **NextAuth v5** + **Google OAuth**
- Session-aware routing (redirect to `/app` when logged in)
- Global state with **Zustand** for chat/session UI state

---

## 🧱 Tech Stack

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS, custom CSS, `globals.css`
- **State Management**: Zustand
- **Auth**: NextAuth v5 (Google Provider)
- **DB / ORM**: MongoDB + Mongoose
- **UI / UX**: Framer Motion, custom components, `react-icons`, tooltips, drawers
- **AI SDK**: `@google/generative-ai`
- **Markdown & Editor**: `react-markdown`, TipTap + lowlight + highlight.js
- **Notifications**: `sonner`
- **Infra / DevOps**:
  - Docker & Docker Compose
  - Kubernetes on **kind** (local) or any K8s cluster
  - Nginx Ingress + cert-manager (Let’s Encrypt TLS)
  - Jenkins Helm chart (controller + agents) for CI/CD


---

## 📂 Project Structure (High Level)

- `src/app` – Next.js App Router pages
  - `page.tsx` – Landing page with GitHub and "Try Now" CTA
  - `(routes)/(general)/app` – Authenticated app shell & chat routes
  - `api/auth/[...nextauth]/route.ts` – NextAuth v5 API route
- `src/components` – All UI components
  - `chat-provider-components/` – Chat UI, loaders, code blocks, TTS/STT, share, etc.
  - `header-components/` – App header, logo, sign-in, top loader
  - `sidebar-components/` – Chat list, theme switch, sidebar layout
  - `input-prompt-components/` – Prompt input box & actions
  - `prompt-gallery-components/` – Prompt cards & gallery
  - `dev-components/` – Reusable design system primitives
- `src/utils` – DB connection, Zustand store, theme providers, emoji & prompt data
- `src/models` – `user.model.ts`, `chat.model.ts` (Mongoose schemas)
- `kind/` – Kubernetes manifests (Deployment, Service, Ingress, HPA, PVC, MongoDB, Nginx, Secrets, ConfigMap, Namespace)
- `jenkins/` & `GitOps/` – Jenkins pipeline + GitOps layout

For a more UI-focused description, see **ABOUT_APP.md**.

---

## 🔑 Environment Variables

All production env setup is documented in **ENV_SETUP.md**. Summary of required keys:

- `GOOGLE_ID` – Google OAuth Client ID
- `GOOGLE_SECRET` – Google OAuth Client Secret
- `MONGODB_URI` – MongoDB connection string (Atlas recommended)
- `NEXTAUTH_SECRET` – NextAuth secret (use `npx auth secret` to generate)
- `NEXTAUTH_URL` – Base URL of your deployed app
- `NEXT_PUBLIC_API_KEY` – Public API key for Google Generative AI

Create a `.env.local` for local development:

```bash
GOOGLE_ID=your_google_client_id
GOOGLE_SECRET=your_google_client_secret
MONGODB_URI=your_mongodb_uri
NEXTAUTH_SECRET=your_generated_secret
NEXTAUTH_URL=http://localhost:3000
NEXT_PUBLIC_API_KEY=your_google_generative_ai_key
```

> ⚠️ Never commit `.env*` files to Git.

---

## 🧑‍💻 Local Development

### 1. Install Dependencies

```bash
npm install
# or
yarn
# or
pnpm install
```

### 2. Set Up Env

Create `.env.local` as shown above.

### 3. Run Dev Server

```bash
npm run dev
```

Then open: http://localhost:3000

---

## 🐳 Docker & Docker Compose

### Build Image

```bash
docker build -t your-dockerhub-username/dev-gemini-clone:latest .
```

### Run Container

```bash
docker run -p 3000:3000 --env-file .env.production \
  your-dockerhub-username/dev-gemini-clone:latest
```

### Using Docker Compose

If you prefer Compose (see `docker-compose.yml`):

```bash
docker-compose up --build
```

---

## ☸️ Kubernetes (kind / any cluster)

Kubernetes manifests live in `kind/`. They cover:

- `gemini-deployment.yml` – Next.js app Deployment (replicas, resources, env)
- `gemini-service.yml` – NodePort Service on port 3000
- `gemini-ingress.yml` – Nginx Ingress with TLS via cert-manager
- `mongodb-*.yml` – MongoDB Deployment + Service
- `nginx-*.yml` – Nginx ingress controller
- `configmap.yml` – Non-secret env vars (IDs, URLs, etc.)
- `secrets.yml` – Encrypted secrets (Google, NextAuth, API key)
- `persistent-volume*.yml` – Storage for MongoDB
- `gemini-hpa.yml` – Horizontal Pod Autoscaler config
- `gemini-namespace.yml` – Dedicated namespace: `gemini-namespace`

### Example: Apply Manifests

```bash
# Create namespace
kubectl apply -f kind/gemini-namespace.yml

# Config & secrets
kubectl apply -f kind/configmap.yml
kubectl apply -f kind/secrets.yml

# Storage & DB
kubectl apply -f kind/persistent-volume.yml
kubectl apply -f kind/persistent-volume-claim.yml
kubectl apply -f kind/mongodb-deployment.yml
kubectl apply -f kind/mongodb-service.yml

# App & ingress
kubectl apply -f kind/gemini-deployment.yml
kubectl apply -f kind/gemini-service.yml
kubectl apply -f kind/nginx-deployment.yml
kubectl apply -f kind/nginx-service.yml
kubectl apply -f kind/gemini-ingress.yml
```

Once DNS / nip.io and TLS are configured, you can access the app via the host configured in `gemini-ingress.yml`.

---

## 🧪 CI/CD with Jenkins

The `jenkins/` folder shows how to run **Jenkins on Kubernetes** using Helm, including controller + agents.

### Quick Start (from jenkins/README.md)

```bash
helm repo add jenkins https://charts.jenkins.io
helm repo update

kubectl create ns jenkins

helm install jenkins jenkins/jenkins -n jenkins -f values.yaml
```

Then forward the service and open the UI:

```bash
kubectl port-forward svc/jenkins -n jenkins 8080:8080
# http://localhost:8080
```

You can wire the provided Jenkinsfile(s) to:

- Build the Docker image
- Push to Docker Hub
- Deploy to your Kubernetes cluster (GitOps style via `GitOps/` if desired)

---

## 🎯 DevOps Skills Demonstrated

This project demonstrates hands-on experience with:

- Kubernetes cluster deployment and management
- CI/CD pipeline automation using Jenkins
- Docker containerization and optimization
- Kubernetes autoscaling using HPA
- Secure configuration using ConfigMaps and Secrets
- Ingress controller and SSL setup using Nginx and cert-manager
- GitOps-based deployment workflow
- Production-grade application deployment

---

## 🧭 Key User Flows

- Visit `/` – Landing page with **GitHub** button and **Try Now** CTA
- Click **Try Now** → `/app` – If not signed in, you’ll be asked to authenticate
- Sign in with Google → redirected to **main chat UI**
- Start chatting, manage chats, explore prompt gallery, use TTS/STT, etc.

---

## 🤝 Contributing

Suggestions, issues, and PRs are welcome.

- Fork the repo
- Create a feature branch
- Commit with clear messages
- Open a pull request describing your change

---

## 📄 License

This project is for educational and portfolio/demo purposes. Adapt the license section to your own needs if you plan to open-source or commercialize it.

---

## 👨‍💻 Author

**Muhammad Taha Azhar**  
Cloud & DevOps Engineer

- **GitHub:** https://github.com/ChaudharyTaha142
- **LinkedIn:** https://www.linkedin.com/in/muhmmad-taha-azhar/
