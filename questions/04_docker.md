# 04 – Docker

Discusses container basics, Dockerfiles, and best practices.

## Table of Contents
1. Docker vs Container
2. Dockerfile: ENTRYPOINT vs CMD
3. Image Size Optimization
4. Build-time vs Runtime Secrets
5. Reducing Docker Build Time
6. Docker-in-Docker or Alternatives
7. Other Container Build Tools
8. **Scenario: Kaniko Image Build Failing Without Docker Daemon**
9. (Optional) RBAC for Kaniko? (See `05_kubernetes.md` for RBAC if needed)

---

## 1) Docker vs Container
**Question:**  
What’s the difference between Docker as a tool and the concept of a container?

<details>
  <summary>Hints / Key Points</summary>

  - **Docker** is a platform for building/managing containers.
  - A **container** is an isolated environment bundling the app and dependencies.
  - Docker is popular, but other runtimes exist (Podman, Containerd).
</details>

---

## 2) Dockerfile: ENTRYPOINT vs CMD
**Question:**  
A coworker is confused about `ENTRYPOINT` and `CMD` in a Dockerfile. How do you explain the difference?

<details>
  <summary>Hints / Key Points</summary>

  - **ENTRYPOINT**: The main command the container will always run.
  - **CMD**: Default arguments that can be overridden at runtime.
  - Typically, you set `ENTRYPOINT` to the main process and use `CMD` for optional flags.
</details>

---

## 3) Image Size Optimization
**Question (Scenario):**  
You have a huge Docker image based on a full JDK. You want to reduce its size. How do you do it, and why does size matter?

<details>
  <summary>Hints / Key Points</summary>

  - Use **multi-stage builds** or switch to a smaller base (JRE or Alpine).
  - Clean up leftover artifacts (logs, caches).
  - Smaller images pull faster, less storage overhead, fewer security risks.
</details>

---

## 4) Build-time vs Runtime Secrets
**Question:**  
You need to use some private tokens or credentials during the build. How do you add them without exposing them in the final image?

<details>
  <summary>Hints / Key Points</summary>

  - **ARG** for build-time secrets (not present in the final image).
  - Inject secrets at runtime via environment variables or secret managers.
  - Don’t store secrets in plain text in the Dockerfile or version control.
</details>

---

## 5) Reducing Docker Build Time
**Question (Scenario):**  
Your Docker builds take too long, especially for .NET or Java projects. How can you make them faster?

<details>
  <summary>Hints / Key Points</summary>

  - Reorder Dockerfile steps to install dependencies first, so you can cache them.
  - Use multi-stage builds to keep final images small.
  - Possibly store or share a build cache between CI runs.
</details>

---

## 6) Docker-in-Docker or Alternatives
**Question:**  
Sometimes we build Docker images inside a container during CI. Why do we do that, and what are some alternatives?

<details>
  <summary>Hints / Key Points</summary>

  - **Docker-in-Docker**: runs a Docker daemon inside a container, but can be less secure.
  - Alternatives: **Kaniko**, **Buildah**, **Podman** to build without a Docker daemon.
  - Reduces the need for privileged mode in CI.
</details>

---

## 7) Other Container Build Tools
**Question:**  
If Docker wasn’t an option, what else could you use to build and run containers?

<details>
  <summary>Hints / Key Points</summary>

  - **Podman**, **Buildah**, **Containerd**.
  - For Java, **Jib** can build containers without a Docker daemon.
  - Some environments rely on containerd or rkt (less common nowadays).
</details>

---

## 8) Scenario: Kaniko Image Build Failing Without Docker Daemon
**Question:**  
You are using **Kaniko** to build and push Docker images in a Kubernetes Pod, but the build fails due to the absence of a Docker daemon.

- What steps would you take to troubleshoot Kaniko’s failure?
- How can you configure it to build images without a Docker daemon?

<details>
  <summary>Hints / Key Points</summary>

  - Verify the **Kaniko** Pod has access to your Dockerfile, context, and registry credentials.
  - Kaniko doesn’t need a Docker daemon; pass `--context` and `--destination` parameters correctly.
  - Ensure you have the right RBAC permissions if it needs to create or manage certain resources in K8s.
</details>
