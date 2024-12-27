# 07 – Secrets Management

Deals with handling sensitive data like passwords, tokens, and keys in DevOps.

## Table of Contents
1. What Are Secrets & Why
2. Storing and Managing Secrets

---

## 1) What Are Secrets & Why
**Question:**  
Organizations always talk about storing things like passwords or tokens as “secrets.” What’s the big deal?

<details>
  <summary>Hints / Key Points</summary>

  - It keeps sensitive data out of plain text in code or config.  
  - Minimizes risk if repos or logs get exposed.  
  - In Kubernetes, a Secret is base64-encoded, but a real secrets manager provides better security.
</details>

---

## 2) Storing and Managing Secrets
**Question (Scenario):**  
Your team has many credentials for different microservices. How can you safely store and use them without embedding them in code?

<details>
  <summary>Hints / Key Points</summary>

  - Use a **secrets manager** (like HashiCorp Vault, AWS Secrets Manager, Azure Key Vault).  
  - Give each service controlled access.  
  - Automate secret rotation and auditing, especially if you handle sensitive data.
</details>
