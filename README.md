<p align="center">
  <img src="https://raw.githubusercontent.com/argoproj/argo-cd/master/docs/assets/argo.png" alt="Argo CD Logo" width="120"/>
</p>

<h1 align="center">GitOps with Argo CD – Dev / Stage / Prod</h1>

<p align="center">
  <b>Production-style GitOps implementation using Argo CD and Kubernetes</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/GitOps-Argo%20CD-blue"/>
  <img src="https://img.shields.io/badge/Kubernetes-kind-blue"/>
  <img src="https://img.shields.io/badge/Environments-dev%20%7C%20stage%20%7C%20prod-green"/>
  <img src="https://img.shields.io/badge/Status-Healthy%20%26%20Synced-success"/>
</p>

---

## 📌 Overview

This repository demonstrates a **production-grade GitOps workflow** using **Argo CD** to manage Kubernetes deployments across **dev, stage, and prod** environments.

Unlike demo repositories, this project focuses on:

- Environment isolation
- Clear ownership
- Declarative Kubernetes manifests
- Real-world troubleshooting and recovery

Git is treated as the **single source of truth**, and Argo CD continuously reconciles cluster state with Git.

---

## 🔧 Tech Stack

- Kubernetes (kind on AWS EC2)
- Argo CD
- Docker
- GitHub
- Linux (Ubuntu)

---

## 🧱 Architecture Overview

```

GitHub Repository
|
v
Argo CD
|
v
Kubernetes Cluster
├── dev namespace
├── stage namespace
└── prod namespace

````

---

## 📊 GitOps Project Structure & Flow

```mermaid
graph TD
    A[GitHub Repository]

    A --> B[apps directory]
    B --> B1[dev]
    B --> B2[stage]
    B --> B3[prod]

    B1 --> D1[deployment yaml dev one replica]
    B1 --> S1[service yaml dev]

    B2 --> D2[deployment yaml stage two replicas]
    B2 --> S2[service yaml stage]

    B3 --> D3[deployment yaml prod three replicas]
    B3 --> S3[service yaml prod]

    A --> C[argocd directory]
    C --> C1[guestbook dev application]
    C --> C2[guestbook stage application]
    C --> C3[guestbook prod application]

    C1 --> N1[kubernetes namespace dev]
    C2 --> N2[kubernetes namespace stage]
    C3 --> N3[kubernetes namespace prod]

    N1 --> P1[pods]
    N2 --> P2[pods]
    N3 --> P3[pods]
````

---

## 🌍 Environments

| Environment | Namespace | Replicas |
| ----------- | --------- | -------- |
| Dev         | dev       | 1        |
| Stage       | stage     | 2        |
| Prod        | prod      | 3        |

Each environment:

* Runs in its **own namespace**
* Uses **environment-scoped resource names**
* Is managed by a **separate Argo CD Application**

---

## 📁 Repository Structure

```
gitops-argocd-kubernetes/
├── apps/
│   ├── dev/
│   ├── stage/
│   └── prod/
├── argocd/
│   ├── dev-app.yaml
│   ├── stage-app.yaml
│   └── prod-app.yaml
├── docs/
│   ├── architecture.md
│   ├── gitops-flow.md
│   └── troubleshooting.md
└── README.md
```

---

## 🔄 GitOps Workflow

1. Developer commits a change to Git
2. Argo CD detects the change
3. Desired state is applied to Kubernetes
4. Manual changes are reverted (drift correction)
5. Deleted resources are recreated (self-healing)

---

## ✅ Key GitOps Capabilities Demonstrated

* Automated synchronization
* Self-healing
* Drift detection and correction
* Environment isolation
* Declarative deployments
* Safe production refactoring

---

## 🛠 Real-World Issues Solved

This project includes **real incidents and fixes**, not just happy paths:

* ImagePullBackOff due to disk exhaustion
* `No space left on device` on EC2
* Argo CD `SharedResourceWarning`
* Immutable field conflicts
* Missing namespace causing silent sync failure
* Stale Argo CD Application reconciliation
* Invalid Git paths and manifests

All resolutions are documented in **`docs/troubleshooting.md`**.

---

## 📘 References

* Argo CD Documentation
  [https://argo-cd.readthedocs.io/](https://argo-cd.readthedocs.io/)

* Argo CD Example Apps (used only as reference)
  [https://github.com/argoproj/argocd-example-apps](https://github.com/argoproj/argocd-example-apps)

---

## 👤 Author

**Siddu S N**
GitHub: [https://github.com/MrSiddu73](https://github.com/MrSiddu73)

---

## 🏁 Final Status

✅ Dev – Healthy & Synced
✅ Stage – Healthy & Synced
✅ Prod – Healthy & Synced

This repository represents a **complete, production-grade GitOps implementation**.