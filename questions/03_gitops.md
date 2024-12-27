# 03 – GitOps & ArgoCD

Focuses on ArgoCD usage, App-of-Apps, and the GitOps paradigm.

## 1) What is GitOps?
**Question:**  
Describe the GitOps paradigm in your own words.

<details>
  <summary>Hints / Key Points</summary>

  - Managing infrastructure and applications using Git as the source of truth.
  - Automated reconciliation loops (ArgoCD/Flux).
  - Pull-request-based change management.
</details>

---

## 2) ArgoCD Basics
**Question:**  
Why is ArgoCD considered a GitOps tool?

<details>
  <summary>Hints / Key Points</summary>

  - It continuously monitors a Git repo for changes (manifests, Helm charts).
  - Syncs desired state from Git to the cluster, enabling fully declarative deployments.
</details>

---

## 3) App-of-Apps Pattern
**Question:**  
Explain the “App-of-Apps” approach in ArgoCD.

<details>
  <summary>Hints / Key Points</summary>

  - A root ArgoCD Application references other “child” applications (Helm, Kustomize, etc.).
  - Lets you manage multiple apps from a single “umbrella” manifest.
  - Good for large or multi-team environments.
</details>

---

## 4) Adding a New App
**Question:**  
If you have a root “app-of-apps” repo, how do you add a new microservice?

<details>
  <summary>Hints / Key Points</summary>

  - Create a new ArgoCD Application resource referencing the microservice’s Helm chart or manifests.
  - Include it under the root application’s “applications list.”
</details>
