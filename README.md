# GitOps Demo Config ⚙️

Kubernetes manifests for deploying the app using Argo CD.

---

## Overview

This repo defines the desired state of the application.

Argo CD watches this repo and applies changes automatically.

---

## GitOps Model

App repo → build image → update this repo → Argo CD → Kubernetes

Git = source of truth

---

## Structure

k8s/
  base/
  overlays/
    dev/
    prod/

argocd/
  application-dev.yaml

---

## Deployment

Defined in:
argocd/application-dev.yaml

Features:
- automated sync
- self-healing

---

## Flow

1. App repo builds image
2. This repo updates image tag
3. Argo CD detects change
4. Kubernetes applies it

---

## Test

kubectl port-forward svc/gitops-demo 8181:80 -n dev
curl http://localhost:8181/health

---

## Self-healing

kubectl delete pod -l app=gitops-demo -n dev

Argo CD restores state automatically.

---

## Kustomize

base/ → shared  
overlays/dev → 1 replica  
overlays/prod → 2 replicas  

---

## Why GitOps

- Declarative
- Auditable
- Easy rollback
- Drift correction

---

## Related Repo

https://github.com/acordovap/gitops-demo-app
