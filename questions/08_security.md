# 08 – Security

Focuses on adding security checks to CI/CD, avoiding hardcoded secrets, and building secure images.

## Table of Contents
1. Pipeline Security
2. Avoiding Hardcoded Secrets
3. Secure Docker Builds

---

## 1) Pipeline Security
**Question (Scenario):**  
You want to catch vulnerabilities early. How can you add security steps to your CI/CD pipeline?

<details>
  <summary>Hints / Key Points</summary>

  - **Static code analysis** (SAST) to look for known flaws.  
  - **Image scanning** for Docker containers.
  - **SCA scanning** Analyzing open-source and third-party components in the application for vulnerabilities and licensing issues.
  - Dependency checks to flag libraries with known CVEs.
</details>

---

## 2) Avoiding Hardcoded Secrets
**Question:**  
You found actual passwords in your pipeline scripts. How do you clean that up and prevent it from happening again?

<details>
  <summary>Hints / Key Points</summary>

  - Store secrets in a secure variable store or a secrets manager.  
  - Don’t commit them to Git.  
  - Use environment variables or injected secrets at runtime.
</details>

---

## 3) Secure Docker Builds
**Question:**  
Your production app runs in Docker containers. What steps can you take to make sure those containers are secure?

<details>
  <summary>Hints / Key Points</summary>

  - Use **minimal base images**, patch them regularly.  
  - Don’t run as root if you can avoid it.  
  - Scan images for vulnerabilities before deploying.  
  - Sign images for verification (e.g., with Cosign or Notary).
</details>
