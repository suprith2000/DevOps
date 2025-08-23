## 🌊 What is Flux?

Flux is a **GitOps tool** for Kubernetes.

- It keeps your Kubernetes clusters in sync with configuration stored in **Git (or OCI registries)**.
- Any change you make in Git (or Helm chart, Kustomize, YAML) gets automatically applied to the cluster.

Flux is modular — it has controllers like:

- **Source Controller** (manages Git/Helm/OCI sources)
- **Kustomize Controller** (applies Kustomize overlays)
- **Helm Controller** (manages Helm releases)
- **Notification Controller** (alerts & automation)

---

## 📘 What are Flux Descriptors?

Flux descriptors are **YAML custom resources (CRDs)** that define how Flux behaves.  
They tell Flux:

- Where to fetch the desired state (Git repo, Helm repo, OCI registry)
- How to apply it (Kustomize, Helm, plain manifests)
- How to keep syncing (intervals, retries, health checks)

Basically, **descriptors = declarative configuration files for Flux**.

Each Flux component has its own descriptors (CRDs). They’re Kubernetes objects, so you write them like you would write a Deployment or Service.

---

## 🛠️ Types of Flux Descriptors

Here are the **main descriptors** you’ll encounter:

1. **Source Descriptors** (where to get manifests from)
    
    - `GitRepository` → Points to a Git repo with manifests
    - `HelmRepository` → Points to a Helm chart repo
    - `Bucket` → Fetches from an S3/GCS/Azure blob bucket
    - `OCIRepository` → Fetches from OCI registry (charts, configs, etc.)
    
    👉 Example:
    
```
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: my-app-config
  namespace: flux-system
spec:
  interval: 1m
  url: https://github.com/org/my-app-config
  ref:
    branch: main

```
    

---

2. **Kustomize Descriptors** (how to apply manifests)
    
    - `Kustomization` → Defines how to render and apply a Git source with overlays.
    
    👉 Example:
```
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: my-app
  namespace: flux-system
spec:
  interval: 5m
  path: "./overlays/prod"
  prune: true
  sourceRef:
    kind: GitRepository
    name: my-app-config
```
    

---

3. **Helm Descriptors** (Helm-based deployments)
    
    - `HelmRelease` → Manages Helm chart installation & upgrades
    - `HelmChart` → Defines the chart fetched from a repo (usually auto-managed)
    
    👉 Example:
```
apiVersion: helm.toolkit.fluxcd.io/v2beta1
kind: HelmRelease
metadata:
  name: my-app
  namespace: flux-system
spec:
  interval: 5m
  chart:
    spec:
      chart: my-app-chart
      version: "1.2.3"
      sourceRef:
        kind: HelmRepository
        name: my-helm-repo
  values:
    replicaCount: 3
```
    

---

4. **Notification Descriptors** (alerts & automation)
    
    - `Alert` → Defines notification targets (Slack, Teams, etc.)
    - `Receiver` → Defines how Flux reacts to external events (webhooks)
    - `Provider` → Defines the provider (Slack, MS Teams, Discord, etc.)
    
    👉 Example:
```
apiVersion: notification.toolkit.fluxcd.io/v1
kind: Alert
metadata:
  name: slack-alert
  namespace: flux-system
spec:
  providerRef:
    name: slack-bot
  eventSeverity: info
  eventSources:
    - kind: Kustomization
      name: my-app
```
    

---

## 🔄 Workflow of Descriptors

1. **Source descriptor** fetches config (e.g., GitRepository)
2. **Kustomization/HelmRelease descriptor** applies config
3. **Notification descriptor** reports results
4. Everything is kept in sync on intervals (e.g., every 1m/5m)

---

## 📦 Why Are They Important in DevOps?

- They make **Flux fully declarative** → Infra and app states are version-controlled.
- They replace manual `kubectl apply` → Git is the source of truth.
- They are **auditable** → Any change is a Git commit.
- They are **extensible** → You can combine sources, overlays, and notifications.

---

## 🚀 What You Need to Contribute

If you want to **contribute to a DevOps project with Flux**, here’s what you should know:

1. **YAML skills** – Understand CRDs and how to define descriptors.
2. **Kubernetes basics** – Namespaces, deployments, services.
3. **GitOps flow** – Code lives in Git, Flux applies it, cluster stays in sync.
4. **Flux CLI** – Helps you bootstrap and manage descriptors.
```
flux bootstrap github \
  --owner=my-org \
  --repository=my-repo \
  --branch=main \
  --path=./clusters/my-cluster
```
    
5. **Debugging** – Use `kubectl describe` or `flux get kustomizations` / `flux get sources` to check status.
6. **Best Practices**:
    
    - Keep descriptors in a dedicated repo (infra repo).
    - Use overlays for dev/staging/prod.
    - Secure secrets (use `SealedSecrets` or `SOPS`).
    - Use `interval` wisely (not too frequent).

---

✅ In short: **Flux descriptors are the CRDs (YAML configs) that tell Flux what to sync, from where, and how**. They’re the backbone of GitOps with Flux.