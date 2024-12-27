# 03 – GitOps & ArgoCD

Focuses on GitOps concepts, ArgoCD usage, the app-of-apps pattern, and ApplicationSets.

## Table of Contents
1. What is GitOps?
2. ArgoCD as a GitOps Tool
3. App-of-Apps Pattern
4. Adding a New App Under a Root “Umbrella”
5. ApplicationSet (Uses & Generators)
6. **Scenario: Deprecated APIs Causing ArgoCD Sync Failures**
7. **Scenario: Namespace Conflicts in ArgoCD Applications**

---

## 1) What is GitOps?
**Question:**  
Your manager says, “We should do GitOps!” How do you explain the core idea of GitOps?

<details>
  <summary>Hints / Key Points</summary>

  - Infrastructure and app config in Git as the single source of truth.
  - A tool (ArgoCD) automatically updates the cluster to match Git.
  - All changes go through PRs, so everything is tracked and auditable.
</details>

---

## 2) ArgoCD as a GitOps Tool
**Question:**  
Why is ArgoCD considered a GitOps solution and not just another deployment tool?

<details>
  <summary>Hints / Key Points</summary>

  - Watches a Git repo for changes, automatically syncing them into the cluster.
  - Declarative approach: no manual clicks or imperative commands.
  - Integrates with Helm, Kustomize, or plain YAML.
</details>

---

## 3) App-of-Apps Pattern
**Question (Scenario):**  
You have a bunch of microservices, each with its own repo or chart. You want a single place to manage them. How would you do this in ArgoCD?

<details>
  <summary>Hints / Key Points</summary>

  - Root “umbrella” application referencing multiple child apps.
  - Each child is a separate Helm chart or folder. 
  - App-of-apps keeps everything organized under one main config.
</details>

---

## 4) Adding a New App Under a Root “Umbrella”
**Question:**  
If you already have a root “app-of-apps” that manages several services, how do you add a brand-new microservice?

<details>
  <summary>Hints / Key Points</summary>

  - Create a new ArgoCD “child” Application in the same or separate repo.
  - Reference it in the root app’s YAML so ArgoCD picks it up.
</details>

---

## 5) ApplicationSet (Uses & Generators)
**Question:**  
What is an ApplicationSet in ArgoCD, and when might you use it? Name at least one generator type.

<details>
  <summary>Hints / Key Points</summary>

  - **ApplicationSet** is a CRD that can create multiple ArgoCD Applications automatically.
  - Used for deploying the same app across multiple clusters or generating apps for each folder/branch.
  - Generators: List, Git directory, Cluster, or SCM provider.
</details>

---

## 6) Scenario: Deprecated APIs Causing ArgoCD Sync Failures
**Question:**  
After upgrading Kubernetes, an ArgoCD application fails to sync due to deprecated APIs in its Helm chart (e.g., `extensions/v1beta1` → `apps/v1`).

- How do you identify which APIs are outdated?
- How do you fix them?

<details>
  <summary>Hints / Key Points</summary>

  - Check chart templates for old API references.
  - Replace them with newer versions (`apps/v1`).
  - Tools like **Pluto** or `helm template` can highlight deprecated APIs.
  - Keep charts updated and test in a staging cluster before upgrading production.
</details>

---

## 7) Scenario: Namespace Conflicts in ArgoCD Applications
**Question:**  
Two ArgoCD applications deploy into the same namespace, causing resource conflicts (e.g., overlapping ConfigMaps). One of them fails to sync.

- How would you troubleshoot and resolve it?
- How do you prevent it in the future?

<details>
  <summary>Hints / Key Points</summary>

  - Identify which resources clash by checking logs or ArgoCD sync errors.
  - Move each app into its own namespace for isolation, or rename the conflicting resources.
  - Have a clear naming/namespace strategy so multiple apps don’t step on each other.
</details>
