# Home Assignment 1

**Objective**: Demonstrate end-to-end DevOps skills, from setting up a local environment to configuring CI/CD, containers, and Kubernetes.

---

## Topics / Instructions

### Prerequisites
- Use a web-server application where the config file path is passed via an environment variable.
- Avoid Terraform for infra creation; everything can be local or in-kind/minikube.

---

### 1. CI

- **Branch policy**: Explain how you’d set up and enforce a branch policy.
- **Merge to main**: Why require pull requests? Outline best practices (e.g., code reviews, checks).
- **DRY Pipelines**: Use parameterization or templates to avoid repeating code.
- **Versioning**: 
  - How do you manage application versions after merges?
  - How do you let developers work on branches without bumping the version prematurely?
- **Dockerfile**:
  - Optimize the Dockerfile; possibly integrate CI steps (tests, lint) within it.
  - On PRs, run at least one test (lint/code coverage/unit tests) inside the Docker build.

---

### 2. CD

- **ArgoCD App-of-Apps**:
  - Use something like kind or minikube. No need for Terraform.
  - Deploy and manage your Helm chart via an ArgoCD Application.
  - The ArgoCD Application is itself managed by a root “app-of-apps.”
  - The application should track the latest commit and be managed by the root app.
  - Explain the folder structure and how it all ties together.

---

### 3. Helm / Kubernetes

- **Handling API Deprecations**: Provide examples of how you’d manage deprecations when upgrading K8s.
- **Create a Job**: In your Helm chart, include a “hello world” job that must run first during ArgoCD deployment.
- **Secure Environment Variables**: Ensure certain env vars do not appear in the raw Helm chart for security reasons.
- **Config in Git**: The web server’s configuration is managed from Git/Helm, not stored in the image.

---

## Deliverables

1. A small Git repository showing:
   - The sample application code or Dockerfile
   - A CI pipeline definition (GitHub Actions, Azure Pipelines, or your choice)
   - A Helm chart for deployment
   - ArgoCD manifests if applicable

2. **README** in your repo explaining:
   - How to run or test it locally
   - How to access the deployed app in kind/minikube

3. Explanations of your design decisions in short markdown notes:
   - How you tackled versioning
   - Why you used certain Docker/Helm features
   - How the ArgoCD “app-of-apps” setup is structured

---

## Tips

- Demonstrate best practices (small Docker images, secrets management, no sensitive info in code).
- Keep it simple. This is a local assignment, so ephemeral clusters or local containers are fine.
- Focus on clarity, automation, and an end-to-end approach.

Good luck!