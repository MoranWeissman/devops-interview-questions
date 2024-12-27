# 09 – Shift Left

Idea of doing testing and security earlier in the development process.

## Table of Contents
1. Shift Left Concept
2. Why Shift Left
3. CI/CD Tools for Shift Left
4. Empowering Developers

---

## 1) Shift Left Concept
**Question:**  
What does “Shift Left” mean in software development, and why do we hear about it a lot now?

<details>
  <summary>Hints / Key Points</summary>

  - Do QA/testing/security as early as possible, not at the end.  
  - Helps catch problems sooner, which is cheaper to fix.  
  - Encourages developers to take ownership of quality from the start.
</details>

---

## 2) Why Shift Left
**Question (Scenario):**  
Your testers always find big problems right before release. How could a Shift Left approach help?

<details>
  <summary>Hints / Key Points</summary>

  - If devs run tests and checks on each commit, issues are spotted earlier.  
  - Fewer surprises at the end.  
  - Faster feedback loops and more stable releases.
</details>

---

## 3) CI/CD Tools for Shift Left
**Question:**  
How do tools like Jenkins, GitHub Actions, or Azure Pipelines help a Shift Left approach?

<details>
  <summary>Hints / Key Points</summary>

  - They let you run automated tests and scans on every push or pull request.  
  - If something fails, devs see it right away.  
  - Can even spin up test environments automatically for quick integration checks.
</details>

---

## 4) Empowering Developers
**Question:**  
Some companies give developers full power to define infrastructure (e.g., Helm charts). How does this fit into Shift Left?

<details>
  <summary>Hints / Key Points</summary>

  - Developers can fix both code and deployment configs early on.  
  - No waiting for ops teams to fix environment issues.  
  - Still need guardrails, but it speeds up delivery and fosters more responsibility.
</details>
