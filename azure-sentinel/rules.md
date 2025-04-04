---
hidden: true
---

# Rules

## Analytics Rules — Building and Managing Detections

***

### **Lesson 5.1: Understanding Detection Rules**

**Analytics Rules** in Sentinel are **the heart of automated threat detection**.\
They continuously run your KQL queries and **generate alerts** when suspicious activity is found.

> **SOC Truth:** No detection = no incident = no response.

**Types of Analytics Rules:**

| Rule Type                           | Description                                                               | Use Case                                      |
| ----------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------- |
| **Scheduled Query Rule**            | Runs a custom KQL query on a schedule                                     | Detect brute-force attacks, abnormal logins   |
| **Microsoft Security Rule**         | Auto-ingests alerts from Defender products                                | Defender for Endpoint, Identity, Office 365   |
| **Fusion Rule**                     | Uses ML/AI to correlate low-fidelity signals into high-fidelity incidents | Detect advanced attacks like credential theft |
| **Machine Learning Rule (Preview)** | Custom ML-based anomaly detection                                         | Find new, unknown threat patterns             |

***

### **Lesson 5.2: Creating Scheduled Query Rules**

**How Scheduled Rules Work:**

* Run a KQL query **every X minutes**.
* If the query returns results → **Alert triggers**.
* Configure **alert grouping**, **severity**, **entity mapping**, and **response actions**.

**Steps to Create a Scheduled Rule:**

1. Microsoft Sentinel → **Analytics** → **+ Create → Scheduled query rule**.
2. Define General Info:
   * Name
   * Description
   * Tactics (MITRE ATT\&CK mapping)
3. Set Rule Logic:
   * Paste your KQL query
   * Set lookup window (e.g., last 1 hour)
   * Set frequency (how often the query runs)
4. Set Alert Details:
   * Severity (Informational, Low, Medium, High)
   * Tactics (Initial Access, Persistence, etc.)
   * Alert Enrichment (map fields like Account, IP, Host)
5. Set Automated Responses:
   * Trigger a playbook automatically (optional)
6. Enable the rule.

**Example Rule: Detect Impossible Travel (Logins from distant locations)**

```kql
kqlCopyEditSigninLogs
| extend Location = tostring(LocationDetails.city)
| summarize Locations = make_set(Location) by UserPrincipalName, bin(TimeGenerated, 1h)
| where array_length(Locations) > 1
```

**Alert:** User logs in from two geographically distant places within 1 hour.

***

### **Lesson 5.3: Tuning and Thresholds**

**Problem:**\
Badly tuned rules generate **alert fatigue** — too many low-value alerts.

**Tuning Best Practices:**

* **Thresholds:** Only trigger an alert if an action happens multiple times.
* **Suppression:** Prevent alerting on the same user/device/IP for a cooling-off period.
* **Dynamic Thresholds:** (Preview feature) Sentinel learns "normal" behavior and detects deviations.

**Example: Alert Only on 5+ Failed Logins**

```kql
kqlCopyEditSigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by UserPrincipalName, bin(TimeGenerated, 1h)
| where FailedAttempts >= 5
```

**Alert Grouping:**

* Group alerts by User, IP, Device to reduce incident noise.
* Example: All failed login attempts from the same user/IP within 1 hour → **one** incident.

> **Detection Engineer Tip:**\
> Tune your rules based on real-world attack behaviors — not just "what's possible" but "what's probable."

***

### **Lesson 5.4: Machine Learning and Fusion Rules**

**Fusion Rules:**

* Prebuilt by Microsoft.
* Use AI to correlate multiple low-signal events into **high-confidence** incidents.
* Example: Anomalous login + malicious OAuth app + suspicious file download.

**Enable/Disable Fusion:**

* Microsoft Sentinel → **Settings** → **Fusion Settings**.

**Machine Learning Anomaly Rules (Preview):**

* Use behavioral baselines (e.g., normal logon locations) to detect anomalies.
* Example: **Sign-in from a never-before-seen country** for a user.

> **SOC Tip:**\
> Fusion rules are your "safety net" — they catch advanced attacks that simple detections miss.
