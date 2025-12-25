# Troubleshooting Guide

This document records real issues encountered during implementation and how they were resolved.

---

## Issue: ImagePullBackOff

### Symptoms
- Pods stuck in ImagePullBackOff
- Application health shows Degraded

### Cause
- Disk exhaustion on EC2 node
- Docker unable to pull images

### Resolution
- Cleaned Docker images and volumes
- Re-pulled container image
- Restarted deployment

---

## Issue: No space left on device

### Symptoms
- Git commit failed
- Kubernetes operations failed
- Temporary files could not be created

### Cause
- EC2 root volume filled due to Docker images and logs

### Resolution
- Docker system prune
- Log cleanup
- APT cache cleanup

---

## Issue: SharedResourceWarning in Argo CD

### Symptoms
- Argo CD warning about shared resources
- Multiple applications claiming the same resource

### Cause
- Same resource names used across environments

### Resolution
- Introduced environment-scoped resource names
- Updated labels and selectors per environment

---

## Issue: Sync Failed with Missing State

### Symptoms
- Argo CD application stuck in Missing
- No Kubernetes resources created
- No events in namespace

### Cause
- Invalid or empty manifests in Git path
- Namespace deletion during refactoring

### Resolution
- Recreated namespace
- Fixed manifests
- Recreated Argo CD Application

---

## Issue: Immutable Field Errors

### Symptoms
- Sync failed with immutable field error

### Cause
- Selector and labels modified on an existing Deployment

### Resolution
- Deleted affected resources
- Allowed Argo CD to recreate them cleanly

---

## Lessons Learned

- Always clean cluster-generated metadata from manifests
- Resource renaming requires controlled cleanup
- GitOps failures are often runtime or infrastructure-related
- Logs and events are critical for debugging
```