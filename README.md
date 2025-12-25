## 📁 GitOps Project Structure & Flow

```mermaid
graph TD
    A[GitHub Repo: gitops-argocd-kubernetes]

    A --> B[apps/]
    B --> B1[dev/]
    B --> B2[stage/]
    B --> B3[prod/]

    B1 --> D1[deployment.yaml (1 replica)]
    B1 --> S1[service.yaml]

    B2 --> D2[deployment.yaml (2 replicas)]
    B2 --> S2[service.yaml]

    B3 --> D3[deployment.yaml (3 replicas)]
    B3 --> S3[service.yaml]

    A --> C[argocd/]
    C --> C1[guestbook-dev Application]
    C --> C2[guestbook-stage Application]
    C --> C3[guestbook-prod Application]

    C1 --> N1[K8s Namespace: dev]
    C2 --> N2[K8s Namespace: stage]
    C3 --> N3[K8s Namespace: prod]

    N1 --> P1[Pods]
    N2 --> P2[Pods]
    N3 --> P3[Pods]
