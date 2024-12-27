# 06 – Helm

Focuses on how Helm helps you package and deploy apps with charts, hooks, and templating.

## Table of Contents
1. Chart Resource Requests/Limits
2. Requests vs Limits Differences
3. Sequence of Operations (Hooks)
4. Multiple Jobs Order
5. Dynamic Resource Generation
6. Handling API Deprecations
7. TPL Helper File

---

## 1) Chart Resource Requests/Limits
**Question:**  
Why do we set resource requests and limits in a Helm chart, and how do we manage them across environments?

<details>
  <summary>Hints / Key Points</summary>

  - Ensures pods have the resources they need, and prevents them from hogging CPU/memory.  
  - Helm’s `values.yaml` can set different requests/limits for dev vs prod.  
  - This helps with cost control and cluster stability.
</details>

---

## 2) Requests vs Limits Differences
**Question:**  
What’s the difference between resource requests and limits in Kubernetes, and how does Helm simplify handling them?

<details>
  <summary>Hints / Key Points</summary>

  - **Requests**: guaranteed resources the container is scheduled with.  
  - **Limits**: the maximum resources a container can use.  
  - Helm: can store these values in `values.yaml` and apply them automatically.
</details>

---

## 3) Sequence of Operations (Hooks)
**Question:**  
You want a job to run before your main app starts. How do you do that in Helm?

<details>
  <summary>Hints / Key Points</summary>

  - Use **Helm hooks** (like `pre-install`) on that job.  
  - The job runs first, and only when it’s done do we proceed to install the app.  
  - Hooks can also run after install if needed.
</details>

---

## 4) Multiple Jobs Order
**Question:**  
If you have multiple jobs that each need to run in a certain order, how can Helm handle that?

<details>
  <summary>Hints / Key Points</summary>

  - You can assign **weights** to hooks (lower weight runs first).  
  - Or run them in a single job that goes step by step.  
  - If they’re really separate, you might split them into subcharts.
</details>

---

## 5) Dynamic Resource Generation
**Question:**  
You want to create several similar resources from a list in `values.yaml`. How do you do that with Helm?

<details>
  <summary>Hints / Key Points</summary>

  - Use a `range` in your template: `{{- range .Values.myItems }}`.  
  - Each item in the list can generate its own resource.  
  - Keep repeated code in `_helpers.tpl` for a cleaner chart.
</details>

---

## 6) Handling API Deprecations
**Question:**  
A new Kubernetes version might deprecate older APIs. How do you update your Helm charts to handle that?

<details>
  <summary>Hints / Key Points</summary>

  - Replace old API versions in your templates (e.g. `extensions/v1beta1` → `apps/v1`).  
  - Tools like **pluto** can scan for deprecated manifests.  
  - Always test in a staging cluster before upgrading production.
</details>

---

## 7) TPL Helper File
**Question:**  
What is the `tpl` function in Helm, and why might you use it?

<details>
  <summary>Hints / Key Points</summary>

  - `tpl` lets you treat a string as a Helm template during rendering.  
  - Useful if you have user-provided or nested templates in your values.  
  - You can store partial templates in `_helpers.tpl` and call them with `tpl`.
</details>
