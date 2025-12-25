## Standard Deployment Flow

1. A developer makes a change to Kubernetes manifests in Git
2. The change is committed and pushed to the repository
3. Argo CD detects the Git change
4. Argo CD compares desired state with cluster state
5. Kubernetes resources are created or updated
6. Application reaches the desired state

---

## Example: Scaling an Application

1. Update `replicas` value in the deployment YAML
2. Commit and push the change to Git
3. Argo CD detects the change automatically
4. Only the targeted environment is updated
5. No manual `kubectl scale` is required

---

## Self-Healing Flow

1. A pod is manually deleted from the cluster
2. Kubernetes reports drift from desired state
3. Argo CD detects the drift
4. Argo CD recreates the missing resource automatically

---

## Drift Correction Flow

1. A manual change is made in the cluster (e.g., scaling pods)
2. The change does not exist in Git
3. Argo CD detects the mismatch
4. The cluster is reverted to match Git state

---

## Promotion Strategy

- Dev → Stage → Prod promotion happens via **Git commits**
- No direct cluster access is used for promotion
- Each environment is reconciled independently

---

## Key Takeaways

- Git is always the source of truth
- Argo CD enforces desired state continuously
- Manual cluster changes are temporary
- Git history provides audit and rollback capability
```

---