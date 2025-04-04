---
hidden: true
---

# Workbooks and Reporting

## Workbooks and Reporting

***

### **Lesson 10.1: Overview of Workbooks**

**What are Workbooks in Sentinel?**

**Workbooks = Interactive Dashboards** built from Sentinel log data.

They allow SOC teams to:

* Visualize trends (sign-ins, alerts, incidents)
* Monitor security posture in real time
* Build executive and SOC reports
* Track KPIs like MTTD (Mean Time to Detect) and MTTR (Mean Time to Respond)

**Key Benefit:**\
Instead of digging through raw logs, you see **real-time security insights** at a glance.

***

**Where to Find Workbooks:**

* Microsoft Sentinel → **Workbooks** blade.

**Built-In Workbook Examples:**

| Workbook Name                          | Purpose                                    |
| -------------------------------------- | ------------------------------------------ |
| Azure AD Sign-ins                      | Visualizes user login trends and risks     |
| Office 365 Activity                    | Shows Exchange, SharePoint, Teams activity |
| Microsoft Defender for Endpoint Alerts | Endpoint threat trends                     |
| Azure Firewall Logs                    | Tracks network traffic and blocks          |

***

### **Lesson 10.2: Building Custom Workbooks**

**Steps to Build Your Own Workbook:**

1. Microsoft Sentinel → **Workbooks** → **+ New**.
2. Choose **Blank Workbook**.
3. Add a **Query Control**:
   * Write a KQL query to pull data.
   * Example: Sign-in failures per hour.
4. Choose a **Visualization**:
   * Timechart, pie chart, grid/table, bar chart, etc.
5. Add **Text Controls**:
   * Add explanations, summaries, or instructions to your dashboard.
6. Save and publish your workbook.

***

**Common SOC Use Cases for Custom Workbooks:**

| Use Case                    | Example Visualization                                          |
| --------------------------- | -------------------------------------------------------------- |
| **Failed Sign-ins**         | Timechart showing spikes in failed logins                      |
| **Top Alerted Users**       | Table listing users with most alerts                           |
| **Incident Trends**         | Bar chart showing incidents by severity                        |
| **Phishing Detection Rate** | Pie chart showing proportion of phishing vs. malware incidents |

***

**Example 1: Failed Sign-ins Timechart**

```kql
kqlCopyEditSigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by bin(TimeGenerated, 1h)
| render timechart
```

(Displays failed login attempts over time.)

***

**Example 2: Top Alerted Users Table**

```kql
kqlCopyEditSecurityAlert
| summarize AlertCount = count() by Entities
| top 10 by AlertCount
```

(Lists users or entities with the most triggered alerts.)

***

### **Lesson 10.3: Reporting to Leadership vs SOC Team**

**Two Types of Reports:**

| Audience       | Focus                | Example                                            |
| -------------- | -------------------- | -------------------------------------------------- |
| **SOC Team**   | Operational details  | Failed logins, endpoint infections, open incidents |
| **Leadership** | High-level summaries | Trends, KPIs, overall risk posture                 |

**For SOC Dashboards:**

* Detail matters.
* Show incident timelines, user risk, endpoint risk.

**For Executive Reports:**

* Summarize key numbers.
* Show high-level trends (e.g., "75% reduction in critical incidents after new policy").

***

**Sample Metrics for Reporting:**

| Metric                    | Definition                                                   |
| ------------------------- | ------------------------------------------------------------ |
| **MTTD**                  | Mean Time to Detect (time from incident occurrence to alert) |
| **MTTR**                  | Mean Time to Respond (time from alert to closure)            |
| **Top Attack Techniques** | MITRE ATT\&CK categories most seen                           |
| **Incident Volumes**      | Total incidents by severity                                  |

***

> **SOC Tip:**\
> **Consistency** matters — publish regular workbook reports weekly or monthly.
