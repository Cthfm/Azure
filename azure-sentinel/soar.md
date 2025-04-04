---
hidden: true
---

# SOAR

## Automation and SOAR with Sentinel

***

### **Lesson 8.1: What is SOAR?**

**SOAR = Security Orchestration, Automation, and Response**

**Purpose of SOAR:**

* **Orchestrate** security tools across different platforms.
* **Automate** repetitive tasks to free analysts' time.
* **Respond** faster to incidents (sometimes automatically).

**In Sentinel:**

* **SOAR = Playbooks (Logic Apps) + Automation Rules**

> **Real-World Benefit:**\
> Automating common tasks (like disabling a compromised user) can reduce incident response time from **hours to seconds**.

***

### **Lesson 8.2: Introduction to Playbooks and Logic Apps**

**Playbooks = Workflows built using Azure Logic Apps.**

**Example Use Cases:**

| Use Case                | Playbook Action                        |
| ----------------------- | -------------------------------------- |
| Phishing Email Detected | Isolate the affected device            |
| Impossible Travel Alert | Send a Teams/Slack message to SOC team |
| Malware Detected        | Disable user account in Azure AD       |

**Anatomy of a Playbook:**

* **Trigger:** Starts the workflow (e.g., "When an incident is created").
* **Actions:** Steps to take (e.g., "Send email", "Block IP", "Disable user").

**Popular Playbook Actions:**

* Post message to Microsoft Teams or Slack
* Send approval email
* Isolate device via Microsoft Defender
* Block IP via Firewall
* Disable user account in Azure AD

***

**Example Simple Playbook Flow:**

```
mathematicaCopyEditIncident Created → Check Severity → If High → Send Email to SOC Manager
```

***

### **Lesson 8.3: Building Auto-Remediation Playbooks**

**Steps to Build a Playbook:**

1. Microsoft Sentinel → **Automation** → **Playbooks** → **+ Create**.
2. Select **Automated Logic App**.
3. Add a **Trigger**:
   * Choose "When a response to an Azure Sentinel alert is triggered."
4. Add **Actions**:
   * Search and add actions like "Send email," "Disable account," or "Isolate device."

**Common Playbook Triggers:**

| Trigger                            | Description                     |
| ---------------------------------- | ------------------------------- |
| **When a Sentinel alert triggers** | Immediate response to any alert |
| **When an incident is created**    | Respond after incident grouping |

***

**Example: Disable User on High-Severity Alert**

* Trigger: When an incident with "High" severity is created.
* Action 1: Send approval request to SOC team.
* Action 2 (if approved): Disable the user in Azure AD.

***

**Important: Approval-Based Playbooks**

Not every automation should happen immediately.\
**Approval workflows** ensure a human validates the action before it is performed.

**Approval Example:**

* Alert: High-risk sign-in detected.
* Action: Send an approval email.
* If approved → Disable the user.

***

### **Lesson 8.4: Automation Rules**

**Automation Rules** are Sentinel's native way to trigger actions automatically without needing a full Playbook.

| Feature                | Automation Rules               | Playbooks                    |
| ---------------------- | ------------------------------ | ---------------------------- |
| **Lightweight**        | Yes                            | No                           |
| **Full Orchestration** | No                             | Yes                          |
| **Example**            | Auto-assign incident to a user | Automatically isolate device |

**Common Automation Rule Use Cases:**

* Auto-assign incidents based on severity.
* Auto-close low-severity incidents matching known benign patterns.
* Add a tag like "High Priority" to incidents from critical users.

***

**Example: Auto-Assign Incident Rule**

* If incident severity = High → Assign to "Senior SOC Analyst" group.
