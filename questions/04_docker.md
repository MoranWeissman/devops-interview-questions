# 04 – Docker

All Docker-specific questions: Dockerfiles, containers, best practices, etc.

## 1) Docker vs Container
**Question:**  
What’s the difference between Docker itself and a container?

<details>
  <summary>Hints / Key Points</summary>

  - Docker is a platform/tool for building/managing containers.
  - A container is an isolated runtime environment with everything needed to run an app.
</details>

---

## 2) Dockerfile: ENTRYPOINT vs CMD
**Question:**  
What are the differences between `ENTRYPOINT` and `CMD`, and when would you use each?

<details>
  <summary>Hints / Key Points</summary>

  - `ENTRYPOINT`: A fixed executable that always runs.
  - `CMD`: Default arguments that can be overridden.
</details>

---

## 3) Image Size Optimization
**Question:**  
How do you reduce the size of a large JDK-based Docker image, and why is it important?

<details>
  <summary>Hints / Key Points</summary>

  - Multi-stage builds, smaller base images (e.g., JRE, Alpine).
  - Faster pulls, fewer resources, reduced security surface.
</details>

---

## 4) Build-time vs Runtime Secrets
**Question:**  
What’s the best way to pass secrets at Docker build time? Differentiate `ARG` from `ENV`.

<details>
  <summary>Hints / Key Points</summary>

  - `ARG` is only available at build time and not persisted in the final image.
  - `ENV` persists into the container at runtime.
</details>
