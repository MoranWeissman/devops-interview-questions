# 05 – Kubernetes

Core K8s topics: pods, services, ingress, CRDs, and debugging.

## Table of Contents
1. Deploying a New Application
2. Services vs Ingress
3. CRDs & Operators
4. Logs & Crash Troubleshooting
5. Resource in “Terminating” State
6. Debugging Inside a Container
7. Editing a Resource Live
8. Service-to-Service Communication
9. Sidecar/Init Containers
10. Bonus: Resource Name Limits
11. **Scenario: RBAC Permissions for Kaniko Builds**
12. **Scenario: Kubernetes Pod Logs Lost After Crash**
13. **Scenario: Resource Exhaustion (OOMKills) in Pods**

---

## 1) Deploying a New Application
**Question:**  
If you have a new microservice to run in Kubernetes, what resources do you usually set up?

<details>
  <summary>Hints / Key Points</summary>

  - Usually a **Deployment** (or StatefulSet if stateful) and a **Service**.
  - Possibly an Ingress or LoadBalancer if external access is required.
  - Might use Helm for templating.
</details>

---

## 2) Services vs Ingress
**Question:**  
What does a Service do in Kubernetes, and how is it different from an Ingress?

<details>
  <summary>Hints / Key Points</summary>

  - **Service**: Exposes pods at a stable address, can be ClusterIP, NodePort, or LoadBalancer.
  - **Ingress**: Defines routing rules for HTTP/HTTPS traffic to one or more Services.
</details>

---

## 3) CRDs & Operators
**Question:**  
How do CRDs (Custom Resource Definitions) and Operators help you extend Kubernetes beyond its default features?

<details>
  <summary>Hints / Key Points</summary>

  - A **CRD** adds a new type of object (like “MyDatabase”) to the cluster.
  - An **Operator** watches these CRDs and automates tasks (install, upgrade, manage).
  - Good for complex/stateful apps so K8s can handle them more natively.
</details>

---

## 4) Logs & Crash Troubleshooting
**Question (Scenario):**  
Your app keeps crashing after a few minutes in Kubernetes. How would you check what’s going on?

<details>
  <summary>Hints / Key Points</summary>

  - Inspect logs from the pod/container.
  - Check events or error messages for the pod.
  - See if it’s an OOM kill, code exception, or config problem.
</details>

---

## 5) Resource in “Terminating” State
**Question:**  
Sometimes a pod or other resource is stuck “Terminating” for a long time. Why could that happen, and what might you do?

<details>
  <summary>Hints / Key Points</summary>

  - **Finalizers** might be blocking deletion.
  - The app might not handle termination signals well, so it never exits.
  - You can remove the finalizer or do a force delete if absolutely needed.
</details>

---

## 6) Debugging Inside a Container
**Question:**  
You need to run commands inside a container for debugging. How do you do that in a Kubernetes environment?

<details>
  <summary>Hints / Key Points</summary>

  - Typically use a CLI to exec into the container.
  - If multiple containers, specify which container.
  - Make sure you have the right RBAC privileges.
</details>

---

## 7) Editing a Resource Live
**Question (Scenario):**  
You spot a small config mistake in a live resource. How would you fix it right away in the cluster? What risks might that cause?

<details>
  <summary>Hints / Key Points</summary>

  - You can **edit** the resource in place with the CLI, but that can cause drift from Git or Helm config.
  - If you’re using GitOps, the next sync might overwrite your manual fix.
  - Best practice: fix it in your config repo or chart too.
</details>

---

## 8) Service-to-Service Communication
**Question:**  
How do different services within the same cluster talk to each other?

<details>
  <summary>Hints / Key Points</summary>

  - **Cluster DNS**: `<service-name>.<namespace>.svc.cluster.local`.
  - A Service provides a stable endpoint, even if pod IPs change.
</details>

---

## 9) Sidecar/Init Containers
**Question:**  
What are sidecar containers and init containers, and why might you use them?

<details>
  <summary>Hints / Key Points</summary>

  - **Init** containers run first to do setup tasks (migrations, config).
  - **Sidecar** containers run alongside the main app for logging, proxying, etc.
  - Helps separate concerns in a single pod.
</details>

---

## 10) Bonus: Resource Name Limits
**Question:**  
Is there a name length limit or other format rule for K8s resources?

<details>
  <summary>Hints / Key Points</summary>

  - Usually follows **DNS label** rules (lowercase, up to 63 chars, alphanumeric + dashes).
  - Some resource types might vary slightly, but typically the same constraints apply.
</details>

---

## 11) Scenario: RBAC Permissions for Kaniko Builds
**Question:**  
You’re running an Azure DevOps agent in Kubernetes, which uses Kaniko to build and push Docker images. It’s failing because it can’t create needed resources.

- How would you troubleshoot the missing permissions?
- How can RBAC be configured to give Kaniko the required access?

<details>
  <summary>Hints / Key Points</summary>

  - Check the Pod logs for permission errors (e.g., “forbidden”).
  - Assign a **ServiceAccount** with an appropriate Role/RoleBinding that allows creating ConfigMaps, Pods, etc.
  - Verify that the agent is using this ServiceAccount when building.
</details>

---

## 12) Scenario: Kubernetes Pod Logs Lost After Crash
**Question:**  
A Kubernetes Pod crashes unexpectedly, and its logs are lost because the container restarts too quickly.

- How would you recover logs from a previously crashed container?
- How can you ensure logs are always accessible?

<details>
  <summary>Hints / Key Points</summary>

  - Use the CLI to get logs from the **previous** container instance (`-p` option), if still available.
  - Centralize logs in an external system like ELK, Loki, or FluentD.
  - Ensure your app flushes logs frequently so they aren’t lost on crash.
</details>

---

## 13) Scenario: Resource Exhaustion (OOMKills) in Pods
**Question:**  
A Kubernetes Pod crashes intermittently and is marked as OOMKilled.

- How would you identify the cause of the memory spikes?
- How do you stop the Pod from running out of memory in the future?

<details>
  <summary>Hints / Key Points</summary>

  - Check resource usage with `kubectl top` or a monitoring tool.
  - Increase the memory limit if the app truly needs more, or find memory leaks.
  - Monitor usage over time, maybe use VPA (Vertical Pod Autoscaler) if appropriate.
</details>
