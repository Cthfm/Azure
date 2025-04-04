---
hidden: true
---

# Sentinel Introduction

### **Why Microsoft Sentinel?**

**Microsoft Sentinel** is a **cloud-native SIEM/SOAR** solution designed to detect, investigate, hunt, and respond to threats across cloud and on-premises environments.

**Why use Sentinel?**

* **Cloud-native** (no hardware, auto-scaling)
* **Integrated** with Microsoft 365, Azure, AWS, GCP
* **Built-in AI/ML** for detecting advanced threats (Fusion detection)
* **SOAR capabilities** with automation (Logic Apps)
* **Built-in Threat Intelligence** with Defender TI

**Key for Defenders:**\
Sentinel allows analysts to move faster, automate repetitive tasks, and scale defenses without managing underlying infrastructure.

> **SOC Analysts** triage and monitor alerts.\
> **Incident Responders** investigate and respond.\
> **Detection Engineers** create and tune rules to detect threats early.

***

### **Lesson 1.2: How Sentinel Fits into the Cyber Defense Stack**

**The Modern Cyber Defense Stack includes:**

* **Security Data Sources** (Azure AD, Office 365, AWS, firewalls, EDR tools like Defender for Endpoint)
* **Microsoft Sentinel** (collects, normalizes, correlates, analyzes data)
* **Incident Management** (creates incidents, supports investigation, supports escalation)
* **Automation/Response Layer** (triggers playbooks and responses)

**Visualization:**

```
cssCopyEdit[Logs/Events] → [Sentinel] → [Analytics Rules] → [Incidents] → [Triage] → [Hunting/Investigation] → [Response Automation]
```

**For Defenders:**

* **SOC Analyst:** Lives inside "Incidents", "Logs", "Investigation Graph"
* **Incident Responder:** Investigates complex threats across users, endpoints, apps
* **Detection Engineer:** Monitors detection efficacy, tunes analytics rules, improves coverage

***

### **Lesson 1.3: Core Components of Microsoft Sentinel**

| Component                   | Description                                                     | Importance to Defenders                       |
| --------------------------- | --------------------------------------------------------------- | --------------------------------------------- |
| **Log Analytics Workspace** | Central place where logs are stored and queried                 | Needed to search events, investigate threats  |
| **Connectors**              | Prebuilt integrations to collect data (Azure, AWS, on-premises) | Needed to get telemetry for visibility        |
| **Analytics Rules**         | Logic that triggers alerts when suspicious behavior is detected | Needed to detect attacks                      |
| **Incidents**               | Grouped alerts for investigation and response                   | Needed for triage and incident handling       |
| **Automation (Playbooks)**  | Automated responses triggered by alerts                         | Needed to speed up or auto-remediate threats  |
| **Threat Hunting**          | Proactive search for threats using KQL queries                  | Needed to find attacks missed by rules        |
| **Workbooks**               | Dashboards for visualizing trends and KPIs                      | Needed for SOC reporting and daily monitoring |
| **Threat Intelligence**     | Ingested feeds for detecting known bad indicators               | Needed for detecting known threats faster     |

***

### **Lesson 1.4: Licensing and Pricing Models**

* **Pay-As-You-Go:**\
  Based on **log ingestion** (GB/day) and **retention** beyond free limits.
* **Commitment Tier Pricing:**\
  Pay a fixed monthly fee based on expected data volume, with a discount.
* **Microsoft 365 E5/A5/G5 Licenses:**\
  Some Sentinel functionality is available through M365 licensing (especially Defender alerts).

**Important Cost Factors for Defenders:**

* Every connected log source costs ingestion (\$$$) — critical to optimize.
* Data retention beyond 90 days incurs extra cost.
* Alerts and Incidents do **not** have separate costs — but Automation (playbooks) built on Logic Apps may.

**SOC Tip:**

* Always balance visibility with cost. Collect only the logs that provide _actionable security signals_.

