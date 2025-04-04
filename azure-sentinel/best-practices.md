---
hidden: true
---

# Best Practices

## Best Practices and Tuning for Microsoft Sentinel

***

### **Lesson 11.1: Cost Management Strategies**

**Sentinel Pricing Reminder:**

* You are charged based on **ingested data volume** (GB/day) into the Log Analytics Workspace.
* Data **retention** beyond 90 days costs extra.
* Some **automation** (Logic Apps) may also generate Azure charges.

**Cost-Saving Best Practices:**

| Tip                         | Explanation                                                          |
| --------------------------- | -------------------------------------------------------------------- |
| **Filter log ingestion**    | Only collect logs you actually need for security.                    |
| **Sample high-volume logs** | Example: Only ingest selected Firewall events, not every packet.     |
| **Use Basic Logs**          | Archive less-critical logs at cheaper rates (e.g., Diagnostic Logs). |
| **Retention Policies**      | Set lower retention for noisy, non-critical logs.                    |
| **Commitment Tiers**        | Pre-pay for expected ingestion volume at a discount.                 |

> **SOC Reality:**\
> **Not every log is worth the cost** — be strategic about what you collect.

***

### **Lesson 11.2: Log Ingestion Best Practices**

**Collect Logs That Support Security Use Cases:**

| Critical Logs           | Why You Need Them                |
| ----------------------- | -------------------------------- |
| **Azure AD Sign-ins**   | Detect account compromise        |
| **Audit Logs**          | Track admin actions              |
| **OfficeActivity Logs** | Detect phishing, insider threats |
| **Defender Alerts**     | Endpoint protection alerts       |
| **Firewall Logs**       | Detect C2 traffic, exfiltration  |
| **Syslog (Linux)**      | Detect server compromises        |

**Avoid Collecting:**

* Verbose system logs with no security value.
* Raw telemetry from apps unless tied to security use cases.

**Tip:**\
Before connecting a new data source, ask:\
&#xNAN;**"How will this log help me detect or investigate an attack?"**

***

### **Lesson 11.3: Tuning Detections to Reduce Noise**

**Alert Fatigue is Real:**

* Too many false positives = overwhelmed analysts.
* Real attacks can get buried in noise.

**Tuning Techniques:**

| Technique              | Example                                                      |
| ---------------------- | ------------------------------------------------------------ |
| **Thresholds**         | Only alert if failed logins > 5 times in 10 minutes.         |
| **Suppression**        | Do not alert again on the same user/device within 1 hour.    |
| **Dynamic Thresholds** | Learn "normal" behavior and detect deviations.               |
| **Entity Mapping**     | Always enrich alerts with User, IP, Host to provide context. |
| **Exclusion Lists**    | Suppress known safe applications/users/devices.              |

***

**Real-World Example: Tuning a Rule**

Original:

```kql
kqlCopyEditSigninLogs
| where ResultType != 0
```

(Alerts on **every** failed login.)

**Tuned:**

```kql
kqlCopyEditSigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by UserPrincipalName, bin(TimeGenerated, 10m)
| where FailedAttempts > 5
```

(Alert only if **5+ failures** in **10 minutes**.)

***

**SOC Tuning Routine:**

1. Review all active incidents every week.
2. Identify false positives.
3. Adjust thresholds, suppression rules, or exclusions.
4. Document tuning changes.

> **Detection Engineering Tip:**\
> **Tuning is a continuous process** — always adapt based on real-world feedback.

***

### **Lesson 11.4: Scaling and Maintaining Sentinel**

**Scaling Tips:**

* **Multiple Workspaces:** Use separate workspaces for Production vs Testing.
* **Table Plans:** Monitor expensive tables (e.g., `Heartbeat`, `Perf`) and optimize.
* **Watch High-Volume Connectors:** Firewall logs, DNS logs can spike ingestion costs.

**Maintenance Best Practices:**

| Task                            | Frequency | Purpose                                     |
| ------------------------------- | --------- | ------------------------------------------- |
| **Review Analytics Rules**      | Monthly   | Remove outdated rules, tune thresholds      |
| **Update Hunting Queries**      | Monthly   | Add new TTPs from threat intelligence       |
| **Audit Permissions**           | Quarterly | Remove unnecessary access                   |
| **Update Playbooks**            | Monthly   | Validate they still work and optimize flows |
| **Review Workbooks/Dashboards** | Monthly   | Ensure dashboards show relevant data        |

***

**Common Pitfalls to Avoid:**

* Letting old, unused rules continue firing.
* Forgetting to close false positive incidents.
* Collecting logs that have no mapped detection or hunting use case.
