# 03 – GitOps & ArgoCD

Covers GitOps concepts, how ArgoCD fits into that model, app-of-apps, and ApplicationSets.

## Table of Contents
1. What is GitOps?
2. ArgoCD as a GitOps Tool
3. App-of-Apps Pattern
4. Adding a New App Under a Root “Umbrella”
5. ApplicationSet (Uses & Generators)

---

## 1) What is GitOps?
**Question:**  
Your manager says, “We should do GitOps!” How do you explain the core idea of GitOps?

<details>
  <summary>Hints / Key Points</summary>

  - Keep your infrastructure and app config in Git, so it’s the single source of truth.  
  - A tool (like ArgoCD) continuously checks Git and updates the cluster so it matches what’s in Git.  
  - All changes go through pull requests, which is easier for review and auditing.
</details>

---

## 2) ArgoCD as a GitOps Tool
**Question:**  
Why is ArgoCD considered a GitOps solution and not just another deployment tool?

<details>
  <summary>Hints / Key Points</summary>

  - It watches a Git repo, and whenever something changes, it updates the cluster.  
  - Everything is declared in code (no manual clicks in a UI).  
  - Helps with version control, rollbacks, and history of changes.
</details>

---

## 3) App-of-Apps Pattern
**Question (Scenario):**  
You have a bunch of microservices, each with its own repo or chart. You want a single place to manage them. How would you do this in ArgoCD?

<details>
  <summary>Hints / Key Points</summary>

  - Have a **root application** (the “umbrella”) that points to multiple child apps.  
  - Each child can be a separate Helm chart or YAML folder.  
  - This root “app-of-apps” approach makes it easy to manage many services at once.
</details>

---

## 4) Adding a New App Under a Root “Umbrella”
**Question:**  
If you already have a root “app-of-apps” that manages several services, how do you add a brand-new microservice?

<details>
  <summary>Hints / Key Points</summary>

  - Create a new ArgoCD “child” Application referencing your new service’s repo or chart.  
  - Add that new Application to the root “app-of-apps” so ArgoCD picks it up automatically.
</details>

---

## 5) ApplicationSet (Uses & Generators)
**Question:**  
What is an ApplicationSet in ArgoCD, why might you use it, and can you name at least one generator type?

<details>
  <summary>Hints / Key Points</summary>

  - An **ApplicationSet** is a CRD that can create many ArgoCD Applications automatically.  
  - Good if you want the same app in multiple clusters or environments, or want to create apps for every folder in a repo.  
  - **Generators**: List, Git directory, Cluster, or SCM provider. For example, the Cluster generator can create apps whenever you add a new cluster.
</details>
