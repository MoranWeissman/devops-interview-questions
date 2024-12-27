# 08 – Security

Security-related questions for CI/CD, containers, scanning, etc.

## 1) Pipeline Security
**Question:**  
What are some examples of implementing security measures in a CI/CD pipeline?

<details>
  <summary>Hints / Key Points</summary>

  - Static Application Security Testing (SAST).
  - Container image scanning for vulnerabilities.
  - Dependency scanning for known CVEs.
</details>

---

## 2) Avoiding Hardcoded Secrets
**Question:**  
How do you prevent secrets from being hardcoded in code or pipelines?

<details>
  <summary>Hints / Key Points</summary>

  - Use external secret managers or environment variable injection.
  - Vault, AWS Secrets Manager, or encrypted variable stores.
</details>

---

## 3) Secure Docker Builds
**Question:**  
Best practices for securing Docker images?

<details>
  <summary>Hints / Key Points</summary>

  - Use minimal base images (e.g., Alpine).
  - Run as non-root, apply security patches regularly.
  - Scan images for vulnerabilities before pushing to production.
</details>
