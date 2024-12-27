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

---

## 1) Docker vs Container
**Question:**  
What’s the difference between Docker as a tool and the concept of a container?

<details>
  <summary>Hints / Key Points</summary>

  - **Docker** is a platform for building and managing containers.  
  - A **container** is basically an isolated environment that holds everything an app needs to run.  
  - Docker is popular, but there are other container runtimes too.
</details>

---

## 2) Dockerfile: ENTRYPOINT vs CMD
**Question:**  
A coworker is confused about `ENTRYPOINT` and `CMD` in a Dockerfile. How do you explain the difference?

<details>
  <summary>Hints / Key Points</summary>

  - **ENTRYPOINT**: The main command the container will always run.  
  - **CMD**: Default arguments or parameters that can be overridden.  
  - Usually you set `ENTRYPOINT` to the main process and `CMD` to any optional flags.
</details>

---

## 3) Image Size Optimization
**Question (Scenario):**  
You have a huge Docker image based on a full JDK. You want to reduce its size. How do you do it, and why does size matter?

<details>
  <summary>Hints / Key Points</summary>

  - Use **multi-stage builds**, or switch to a smaller base (like a JRE or Alpine).  
  - Clean up build caches or unnecessary files.  
  - Smaller images pull and start faster, and are usually more secure (less surface area).
</details>

---

## 4) Build-time vs Runtime Secrets
**Question:**  
You need to use some private tokens or credentials during the build. How do you add them without exposing them in the final image?

<details>
  <summary>Hints / Key Points</summary>

  - **ARG** for build-time secrets (not kept in the finished image).  
  - Or inject secrets at runtime using environment variables.  
  - Don’t store secrets in plaintext in the Dockerfile or version control.
</details>

---

## 5) Reducing Docker Build Time
**Question (Scenario):**  
Your Docker builds take too long, especially for .NET or Java projects. How can you make them faster?

<details>
  <summary>Hints / Key Points</summary>

  - Arrange Dockerfile steps so you install dependencies first (which won’t change often).  
  - Cache layers so you don’t rebuild the entire image every time.  
  - Use multi-stage builds to keep final images small.
</details>

---

## 6) Docker-in-Docker or Alternatives
**Question:**  
Sometimes we build Docker images inside a container during CI. Why do we do that, and what are some alternatives?

<details>
  <summary>Hints / Key Points</summary>

  - **Docker-in-Docker** can help if you don’t have direct access to a Docker daemon.  
  - But it needs privileged mode, which can be less secure.  
  - Alternatives: **Kaniko**, **Buildah**, or **Podman**, which can build images without needing a full Docker daemon.
</details>

---

## 7) Other Container Build Tools
**Question:**  
If Docker wasn’t an option, what else could you use to build and run containers?

<details>
  <summary>Hints / Key Points</summary>

  - **Podman**, **Buildah**, or **Containerd** under the hood.  
  - For Java, **Jib** can build containers natively.  
  - Some environments rely on Docker-like tools but aren’t strictly Docker.
</details>
