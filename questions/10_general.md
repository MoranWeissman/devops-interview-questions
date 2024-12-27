# 10 – General / Architecture

Covers broader DevOps or architecture topics.

## Table of Contents
1. Stateless vs Stateful
2. DevOps Culture
3. Scenario: Handling a Critical Outage
4. Additional General Questions

---

## 1) Stateless vs Stateful
**Question:**  
What’s the main difference between stateless and stateful apps, and how does this affect scaling?

<details>
  <summary>Hints / Key Points</summary>

  - **Stateless**: Doesn’t keep data in memory across requests; easier to scale horizontally.  
  - **Stateful**: Maintains sessions or data that might need external storage. Harder to scale.  
  - Many modern microservices aim to be stateless for simplicity.
</details>

---

## 2) DevOps Culture
**Question:**  
How would you describe “DevOps culture,” and what does it change compared to older dev-and-ops silos?

<details>
  <summary>Hints / Key Points</summary>

  - Focus on **collaboration** and **automation**.  
  - Shared responsibility for stability, performance, and delivery.  
  - Closer feedback loops, continuous integration, continuous delivery.
</details>

---

## 3) Scenario: Handling a Critical Outage
**Question (Scenario):**  
Production goes down during peak hours. Describe how you’d handle the incident, from detecting the problem to resolving it.

<details>
  <summary>Hints / Key Points</summary>

  - **Quick triage**: check logs, monitoring, recent changes, and alerts.  
  - Possibly roll back the last deployment if that caused it.  
  - Communicate clearly with stakeholders.  
  - After fixing, do a post-mortem to learn from it.
</details>

---

## 4) Additional General Questions
- *(Placeholder for any other broad DevOps or architecture topics.)*
