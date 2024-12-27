# 06 – Helm

Helm chart usage, templating, hooks, etc.

## Table of Contents
1. Chart Resource Requests/Limits
2. Requests vs Limits Differences
3. Sequence of Operations (Hooks)
4. Multiple Jobs Order
5. Dynamic Resource Generation
6. Handling API Deprecations
7. TPL Helper File
8. (Optional) Scenario: Deprecated APIs Causing ArgoCD Sync Failures w/ Helm

---

## 1) Chart Resource Requests/Limits
**Question:**  
Why do we set resource requests and limits in a Helm chart, and how do we manage them across environments?

<details>
  <summary>Hints / Key Points</summary>

  - Ensures pods have enough CPU/memory, prevents resource hogging.
  - Helm `values.yaml` can differ for dev vs prod.
  - Good for cost control and stability.
</details>

---

## 2) Requests vs Limits Differences
**Question:**  
What’s the difference between resource requests and limits in Kubernetes, and how does Helm simplify handling them?

<details>
  <summary>Hints / Key Points</summary>

  - **Requests**: minimum guaranteed resources.
  - **Limits**: maximum allowed before throttling or OOMKill.
  - Helm: store these in `values.yaml` for easy environment overrides.
</details>

---

## 3) Sequence of Operations (Hooks)
**Question:**  
You want a job to run before your main app starts. How do you do that in Helm?

<details>
  <summary>Hints / Key Points</summary>

  - Use **Helm hooks** (`pre-install`, `post-install`) on that job.
  - The job runs first; if it succeeds, Helm proceeds to install the rest.
  - Weights can fine-tune the order of multiple hooks.
</details>

---

## 4) Multiple Jobs Order
**Question:**  
If you have multiple jobs that need to run in a certain sequence, how can Helm handle that?

<details>
  <summary>Hints / Key Points</summary>

  - Hooks with **weights** (lower weight runs first).
  - Or a single job that does tasks in order.
  - Sometimes separate subcharts if they’re truly independent.
</details>

---

## 5) Dynamic Resource Generation
**Question:**  
You want to create several similar resources from a list in `values.yaml`. How do you do that with Helm?

<details>
  <summary>Hints / Key Points</summary>

  - Use `{{- range .Values.myItems }}` in the template.
  - Each item in the list gets its own resource.
  - `_helpers.tpl` can keep repeated logic DRY.
</details>

---

## 6) Handling API Deprecations
**Question:**  
A new Kubernetes version might deprecate older APIs. How do you update your Helm charts to handle that?

<details>
  <summary>Hints / Key Points</summary>

  - Replace old references (e.g., `extensions/v1beta1`) with `apps/v1`.
  - Tools like **pluto** can scan for deprecated usage.
  - Test in a lower environment or staging cluster first.
</details>

---

## 7) TPL Helper File
**Question:**  
What is the `tpl` function in Helm, and why might you use it?

<details>
  <summary>Hints / Key Points</summary>

  - `tpl` parses a string as a Helm template at runtime.
  - Good for user-provided or nested templates in `values.yaml`.
  - Keep advanced logic or partials in `_helpers.tpl`.
</details>

---

## 8) (Optional) Scenario: Deprecated APIs Causing ArgoCD Sync Failures w/ Helm
**Question:**  
After upgrading the cluster, your Helm chart can’t sync in ArgoCD because it references deprecated APIs.

- How do you find which APIs are outdated?
- How do you fix them in your chart?

<details>
  <summary>Hints / Key Points</summary>

  - Look at the chart’s templates for older API versions (e.g., `extensions/v1beta1`).
  - Update them to the newer equivalents (e.g., `apps/v1`).
  - **Helm 3.12+** offers a **server-side dry run** via:
    ```bash
    helm upgrade --dry-run=server ...
    ```
    This checks the manifests against the actual cluster APIs, catching potential deprecations or validation issues before you apply them.
  - You can also use tools like **Pluto** to scan for deprecated or removed APIs. 
  - Test in a non-production cluster to confirm everything works with the new APIs.
</details>
