---
hidden: true
---

# Threat Hunting in Sentinel

## Threat Hunting in Microsoft Sentinel

***

### **Lesson 9.1: Threat Hunting Concepts**

**What is Threat Hunting?**

**Threat Hunting = Proactive Search** for attackers who might already be inside your environment.

**Key Difference:**

| Reactive (Traditional SOC) | Proactive (Threat Hunting)        |
| -------------------------- | --------------------------------- |
| Waits for alerts           | Seeks out suspicious activity     |
| Depends on rules           | Assumes attacker may bypass rules |
| Alert → Investigation      | Hypothesis → Investigation        |

**Mindset of a Threat Hunter:**

* Assume you are already compromised.
* Trust nothing; verify everything.
* Search for abnormal behaviors, not just known signatures.

> **SOC Reality:**\
> Detections will **miss things** — that's why you hunt.

***

### **Lesson 9.2: Using Built-in Hunting Queries**

**Microsoft Sentinel** provides dozens of **pre-built hunting queries** organized around **MITRE ATT\&CK tactics**.

**How to Access:**

* Sentinel → **Hunting** → **Built-in Queries**.

**Pre-Built Categories:**

| Category                 | Examples                           |
| ------------------------ | ---------------------------------- |
| **Initial Access**       | New cloud application consented    |
| **Execution**            | Suspicious PowerShell commands     |
| **Persistence**          | New service installed on endpoint  |
| **Privilege Escalation** | Admin privilege assignments        |
| **Defense Evasion**      | Clearing Windows event logs        |
| **Command and Control**  | Outbound connection to rare domain |
| **Exfiltration**         | Unusual download volumes           |

**Using a Built-In Hunt:**

1. Select a hunting query.
2. Customize parameters (e.g., timeframe, user/device filters).
3. Run the query manually.
4. Bookmark interesting results for deeper investigation.

> **Tip:** Treat built-in hunts as a **starting point** — not the final answer.

***

### **Lesson 9.3: Creating Custom Hunting Queries**

**Building your own Hunts:**

**Step 1: Form a Hypothesis**\
Example: "If an attacker has compromised an account, they might create email forwarding rules to steal data."

**Step 2: Translate to KQL**

```kql
kqlCopyEditOfficeActivity
| where OperationName == "New-InboxRule"
| where Parameters contains "ForwardTo"
| project TimeGenerated, UserId, Parameters
```

**Step 3: Hunt**

* Run the query across a time range (e.g., last 7 days).
* Bookmark suspicious results.

***

**Custom Hunting Example 2: Admin Role Abuse**

```kql
kqlCopyEditAuditLogs
| where OperationName == "Add member to role"
| where TargetResources contains "Global Administrator"
| project TimeGenerated, InitiatedBy, TargetResources
```

(Finds users who suddenly got admin privileges.)

***

**Custom Hunting Example 3: Impossible Travel**

```kql
kqlCopyEditSigninLogs
| extend loginLocation = tostring(LocationDetails.city)
| summarize Locations = make_set(loginLocation) by UserPrincipalName, bin(TimeGenerated, 1h)
| where array_length(Locations) > 1
```

(Detects users logging in from distant locations in a short time.)

> **Hunter's Mindset Tip:**\
> Focus on behaviors that attackers **must** perform to achieve their goals (e.g., lateral movement, privilege escalation).

***

### **Lesson 9.4: Using Bookmarks and Notebooks**

**Bookmarks:**

* Save interesting results while hunting.
* Add comments about **why** you think it’s suspicious.

**How to Bookmark:**

* After running a hunt → Select rows → Bookmark.
* Tag with **MITRE ATT\&CK tactics** for easier grouping later.

***

**Notebooks:**

* Advanced hunting tool.
* Integrate **KQL**, **Python**, **Threat Intelligence**, and **Machine Learning**.
* Built on **Azure Machine Learning + Jupyter Notebooks**.

**Use Cases for Notebooks:**

* Complex multi-step hunts.
* Visualize timelines of attacker movement.
* Correlate endpoint, identity, and network data.

> **Detection Engineering Tip:**\
> Notebooks are powerful but optional — master KQL hunting first.
