# 06 – Helm

Everything about the Helm CLI, templating, hooks, chart structure, etc.

## 1) Chart Resource Requests/Limits
**Question:**  
Why define resource requests/limits in Helm chart templates?

<details>
  <summary>Hints / Key Points</summary>

  - Ensures pods don’t starve or oversubscribe cluster resources.
  - Helm allows parameterizing values for different environments.
</details>

---

## 2) Requests vs Limits
**Question:**  
What’s the difference?

<details>
  <summary>Hints / Key Points</summary>

  - **Requests**: guaranteed minimum resources.  
  - **Limits**: maximum resources the container can use.
</details>

---

## 3) Sequence of Operations
**Question:**  
How do you ensure certain jobs run before the main deployment?

<details>
  <summary>Hints / Key Points</summary>

  - Helm hooks (`pre-install`, `post-install`) or ordering resources carefully.
  - “Wait” flags, custom labels, or orchestrate with a separate chart if needed.
</details>

---

## 4) Multiple Jobs Order
**Question:**  
How do you manage the execution order of multiple jobs?

<details>
  <summary>Hints / Key Points</summary>

  - Helm hooks with weights, or a single orchestrating job that triggers steps in sequence.
</details>

---

## 5) Dynamic Resource Generation
**Question:**  
How do you generate multiple similar resources from a values file?

<details>
  <summary>Hints / Key Points</summary>

  - Use `range` in a template: `{{- range .Values.myItems }}`.
  - Each item can produce a resource with dynamic metadata/spec fields.
</details>

---

## 6) Handling API Deprecations
**Question:**  
When a new K8s version removes older APIs, how do you adapt Helm charts?

<details>
  <summary>Hints / Key Points</summary>

  - Update to newer API versions in `.yaml` templates.
  - Tools like `helm template` or `pluto` help detect usage of deprecated APIs.
</details>
