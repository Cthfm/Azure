---
hidden: true
---

# Alerts vs Incidents

## Incident Management Deep Dive

***

### **Lesson 7.1: Understanding Incidents vs Alerts**

**Alerts** = Raw detections triggered by analytics rules or external security products.

**Incidents** = One or more alerts **grouped together** for a complete investigation.

| Concept     | Alert                                     | Incident                                                        |
| ----------- | ----------------------------------------- | --------------------------------------------------------------- |
| **Source**  | Single detection (e.g., suspicious login) | Group of related alerts                                         |
| **Purpose** | Notify of an anomaly                      | Enable full investigation workflow                              |
| **Example** | "Impossible travel detected"              | "Account compromised" (based on multiple suspicious activities) |

**Important:**\
SOC Analysts _work incidents_, not just individual alerts.\
Incidents provide the **bigger picture**.

***

### **Lesson 7.2: The Incident Lifecycle in Sentinel**

**Typical Lifecycle:**

| Stage               | Description                                               |
| ------------------- | --------------------------------------------------------- |
| **Created**         | Analytics rule triggers → Incident created                |
| **Triage**          | Analyst evaluates the incident (Is it real?)              |
| **Assignment**      | Assign to responder or team                               |
| **Investigation**   | Deep dive into entities, logs, timelines                  |
| **Escalation**      | Escalate if the incident is real and needs broader action |
| **Resolution**      | Close the incident: True Positive, False Positive, Benign |
| **Lessons Learned** | Improve rules, documentation, workflows                   |

***

**Incident Status Values:**

| Status     | Meaning                                                                    |
| ---------- | -------------------------------------------------------------------------- |
| **New**    | Incident just created                                                      |
| **Active** | Being investigated                                                         |
| **Closed** | Investigation complete (True Positive, False Positive, or Benign Positive) |

**Classifications When Closing:**

* True Positive (Confirmed threat)
* False Positive (Mistaken detection)
* Benign Positive (Expected behavior, not malicious)

> **SOC Best Practice:**\
> Always **classify** incidents when closing them — it helps detection engineers improve rules later!

***

### **Lesson 7.3: Investigating Incidents**

**The Investigation Workflow:**

1. **Review the Incident Details:**
   * Alerts involved
   * Entities involved (user, device, IP, file, URL)
   * Tactics and Techniques (MITRE ATT\&CK)
2. **Pivot on Entities:**
   * From user → to devices → to IPs → to applications
3. **Use the Investigation Graph:**
   * Visual map of the attack.
   * Click on entities to drill into detailed logs.
4. **Hunt Further (if needed):**
   * Write KQL queries to pull deeper activity.
   * Example: If suspicious login → Check for email forwarding rules.

**Key Sentinel Investigation Features:**

* **Entities Panel:** Lists all involved accounts, IPs, devices.
* **Timeline:** Shows the sequence of alerts and events.
* **Investigation Graph:** Visualizes relationships between alerts and entities.
* **Incident Comments:** Analysts can leave notes for other team members.

***

### **Lesson 7.4: Incident Escalation and Assignment**

**Assign Incidents:**

* From **Microsoft Sentinel → Incidents → Assign Incident**.
* Assign to a specific analyst or team based on severity and expertise.

**Escalate Incidents:**

* Use comments or ticketing integration (ServiceNow, Jira) to escalate.
* High-severity incidents should always be escalated quickly to Incident Response teams.

**Priority Tips:**

| Severity | Example                                   | Response Time       |
| -------- | ----------------------------------------- | ------------------- |
| High     | Ransomware alert, C2 traffic              | Immediate (minutes) |
| Medium   | Multiple failed login attempts            | 1-2 hours           |
| Low      | New application sign-in from known device | Same day            |

> **IR Tip:**\
> Always track who owns an incident to ensure **clear accountability**.
