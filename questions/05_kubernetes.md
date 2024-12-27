# 05 – Kubernetes

Covers the basic K8s concepts: pods, services, ingress, CRDs, and commands.

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

---

## 1) Deploying a New Application
**Question:**  
If you have a new microservice to run in Kubernetes, what resources do you usually set up?

<details>
  <summary>Hints / Key Points</summary>

  - Usually a **Deployment** (or StatefulSet, if stateful) and a **Service**.  
  - An Ingress or LoadBalancer if you need external access.  
  - Might use Helm if you want templating.
</details>

---

## 2) Services vs Ingress
**Question:**  
What does a Service do in Kubernetes, and how is it different from an Ingress?

<details>
  <summary>Hints / Key Points</summary>

  - **Service**: Exposes pods at a stable address, can be ClusterIP, NodePort, or LoadBalancer.  
  - **Ingress**: Lets you define routing rules for HTTP/HTTPS traffic to one or more Services.
</details>

---

## 3) CRDs & Operators
**Question:**  
How do CRDs (Custom Resource Definitions) and Operators help you extend Kubernetes beyond its default features?

<details>
  <summary>Hints / Key Points</summary>

  - A **CRD** adds a new type of object (e.g., “MyDatabase”) to the cluster.  
  - An **Operator** watches these CRDs and automates tasks like setting up or managing them.  
  - Good for complex or stateful apps, so K8s can handle them in a more “self-service” way.
</details>

---

## 4) Logs & Crash Troubleshooting
**Question (Scenario):**  
Your app keeps crashing after a few minutes in Kubernetes. How would you check what’s going on?

<details>
  <summary>Hints / Key Points</summary>

  - Look at **logs** from the pod’s container(s).  
  - Check the events or error messages for that pod.  
  - See if it’s an OOM kill, a code issue, or a config problem.
</details>

---

## 5) Resource in “Terminating” State
**Question:**  
Sometimes a pod or other resource is stuck “Terminating” for a long time. Why could that happen, and what might you do?

<details>
  <summary>Hints / Key Points</summary>

  - Could be **finalizers** that aren’t cleaned up.  
  - The app might not handle termination signals well, so it never exits.  
  - You can remove the finalizer or do a force delete if absolutely needed.
</details>

---

## 6) Debugging Inside a Container
**Question:**  
You need to run commands inside a container for debugging. How do you do that in a Kubernetes environment?

<details>
  <summary>Hints / Key Points</summary>

  - Usually you use a CLI tool to run an **exec** into the container.  
  - You might have to specify which container if there’s more than one in the pod.  
  - Permissions (RBAC) might affect who can do this.
</details>

---

## 7) Editing a Resource Live
**Question (Scenario):**  
You spot a small config mistake in a live resource. How would you fix it right away in the cluster? What risks might that cause?

<details>
  <summary>Hints / Key Points</summary>

  - You can **edit** the resource in place, but that can cause drift from your Git or Helm config.  
  - If you’re using GitOps, the next sync might overwrite your live change.  
  - Best practice is to fix it in your config repo or chart too.
</details>

---

## 8) Service-to-Service Communication
**Question:**  
How do different services within the same cluster talk to each other?

<details>
  <summary>Hints / Key Points</summary>

  - They can use the **cluster DNS name**: `<service-name>.<namespace>.svc.cluster.local`.  
  - The Service acts as a stable endpoint, even if pod IPs change.
</details>

---

## 9) Sidecar/Init Containers
**Question:**  
What are sidecar containers and init containers, and why might you use them?

<details>
  <summary>Hints / Key Points</summary>

  - **Init** containers run first to do setup tasks (like migrations or waiting for a dependency).  
  - **Sidecar** containers run alongside the main app for logging, proxying, or monitoring.  
  - They help split responsibilities in a single pod.
</details>

---

## 10) Bonus: Resource Name Limits
**Question:**  
Is there a name length limit or other format rule for K8s resources?

<details>
  <summary>Hints / Key Points</summary>

  - Most resource names follow **DNS label** rules (lowercase, alphanumeric + dashes).  
  - Usually up to 63 characters.  
  - Going past that or using invalid chars will cause validation errors.
</details>
