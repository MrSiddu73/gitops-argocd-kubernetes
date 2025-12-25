# GitOps Architecture

This document describes the architecture of the GitOps system implemented in this repository using **Argo CD** and **Kubernetes**.

---

## High-Level Architecture

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
```

---

## Components

### 1. GitHub Repository
- Acts as the **single source of truth**
- Stores Kubernetes manifests for all environments
- Any change to the system must happen through Git

### 2. Argo CD
- Continuously monitors the Git repository
- Compares desired state (Git) with actual state (cluster)
- Automatically applies changes to Kubernetes
- Performs self-healing and drift correction

### 3. Kubernetes Cluster
- Runs on **kind inside AWS EC2**
- Hosts three isolated namespaces:
  - `dev`
  - `stage`
  - `prod`
- Each namespace is managed by a separate Argo CD Application

---

## Environment Isolation

Each environment:
- Has its **own namespace**
- Uses **environment-scoped resource names**
- Is managed independently by Argo CD

This prevents:
- Cross-environment interference
- Shared resource ownership issues
- Accidental production impact

---

## Design Principles

- Declarative configuration
- Git-based promotion
- Environment isolation
- Clear ownership boundaries
- Production-safe refactoring

---

## Summary

This architecture follows **GitOps best practices** by enforcing Git as the source of truth and using Argo CD as the reconciliation engine to manage Kubernetes environments safely and consistently.
```