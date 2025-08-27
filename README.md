# 🧠 cv-platform-infra

**cv-platform-infra** Deploys [cv-platform](https://github.com/mtb90/cv-platform) services on K8s.

## Propose:

Is a hands-on project focused on exploring modern DevOps/GitOps practices. It integrates
cutting-edge tools for platform engineering, automation.

---

## 🚀 Project Goals

- Learn and apply DevOps and GitOps methodologies
- Experiment with monitoring tools like (grafana, prometheus)

---

## 🛠️ Tech Stack Overview

### 🔧 DevOps / GitOps

- **Minikube** — Local Kubernetes cluster
  [https://minikube.sigs.k8s.io/docs](https://minikube.sigs.k8s.io/docs)
- **ArgoCD** — Declarative GitOps continuous delivery
  [https://argo-cd.readthedocs.io/en/stable](https://argo-cd.readthedocs.io/en/stable)
- **Argo Workflow** — Kubernetes-native workflow engine
  [https://argoproj.github.io/workflows/](https://argoproj.github.io/workflows/)

---

## 📚 Documentation

- [🏗️ Project Architecture](docs/project_architecture.md)
- [💻 Project Deployment](docs/project_deployment.md)

---

## ✅ Project TODOs

- [x] basi pipeline for testing in github actions
- [x] create base template for ArgoCD
- [x] add postgresql for backend
- [x] deploy simple MinIO to store documents
- [x] add litter for yaml
- [ ] switch from Argo to Temporal
- [ ] deploy Nginx for routing
- [ ] create ingress for backend
- [ ] encrypt secrets in git repo
- [ ] make sure that argo workflows have limited access to other


---

## 📍 Status

This project is a work in progress and intended for learning, prototyping, and experimentation.
