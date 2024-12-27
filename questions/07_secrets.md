# 07 – Secrets Management

Focuses on how to handle sensitive data in DevOps.

## 1) What Are Secrets & Why
**Question:**  
Why do we store credentials as “secrets,” and what does that mean?

<details>
  <summary>Hints / Key Points</summary>

  - Sensitive data like passwords, tokens, API keys.
  - Must be encrypted at rest and in transit.
  - Avoid committing them to git repos.
</details>

---

## 2) Storing and Managing Secrets
**Question:**  
Where do you usually store secrets, and how do you manage them?

<details>
  <summary>Hints / Key Points</summary>

  - Tools: HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, or Kubernetes Secrets (with caution).
  - Implement RBAC, audit logs, and rotation policies.
</details>
