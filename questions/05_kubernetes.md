# 05 – Kubernetes

All general K8s questions: pods, services, Ingress, CRDs, etc.

## 1) Deploying a New Application
**Question:**  
How do you typically deploy a new application into a Kubernetes cluster?

<details>
  <summary>Hints / Key Points</summary>

  - Create YAML manifests (Deployment, Service) or use Helm.
  - `kubectl apply -f` or `helm install`.
  - Proper namespace, resource requests, etc.
</details>

---

## 2) Services vs Ingress
**Question:**  
Explain the difference between a Kubernetes Service and an Ingress.

<details>
  <summary>Hints / Key Points</summary>

  - **Service**: stable networking endpoint for pods.  
  - **Ingress**: higher-level routing, can handle HTTP/HTTPS routes and offload traffic to the right Service.
</details>

---

## 3) CRDs & Operators
**Question:**  
What are CRDs and Operators in Kubernetes, and how do they extend cluster functionality?

<details>
  <summary>Hints / Key Points</summary>

  - **CRD**: custom resource definition, letting you define new resource types.
  - **Operator**: a controller that watches CRDs and automates complex app lifecycles.
</details>

---

## 4) Logs & Crash Troubleshooting
**Question:**  
A Pod is crashing intermittently. How do you retrieve its logs or debug the crash?

<details>
  <summary>Hints / Key Points</summary>

  - `kubectl logs <pod>` or `kubectl logs <pod> -p` for previous container logs.
  - `kubectl describe pod` for events.
  - Possibly a centralized logging solution (EFK stack, Loki, etc.).
</details>

---

## 5) Stuck in Terminating
**Question:**  
When a resource remains in “terminating” status, what can cause that?

<details>
  <summary>Hints / Key Points</summary>

  - Often finalizers are preventing deletion.
  - You may need to edit the resource and remove the finalizer or fix dependent resources first.
</details>
