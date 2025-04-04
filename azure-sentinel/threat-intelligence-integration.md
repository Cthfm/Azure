---
hidden: true
---

# Threat Intelligence Integration

### **What is Threat Intelligence (TI)?**

**Threat Intelligence (TI)** provides **context** about known malicious activity in the wild — such as **IP addresses**, **domains**, **URLs**, **file hashes**, and **actor TTPs** (Tactics, Techniques, Procedures).

**In Microsoft Sentinel:**

* You can **ingest Threat Intelligence** into your workspace.
* You can **correlate incoming logs** with TI indicators to detect threats faster.

**Key TI Examples:**

| Type       | Example           | Threat                     |
| ---------- | ----------------- | -------------------------- |
| IP Address | 45.33.32.156      | Known malware C2 server    |
| Domain     | badsite.com       | Phishing domain            |
| URL        | badsite.com/login | Credential harvesting page |
| File Hash  | 9c3d7d5b9ef63...  | Ransomware executable      |

> **SOC Truth:** Threat intelligence helps you **detect faster** and **respond smarter** because you’re seeing what’s known bad.

***

### **Lesson 6.2: Integrating Threat Intelligence Sources**

**Built-in TI Sources in Sentinel:**

* **Microsoft Defender Threat Intelligence (Defender TI):**
  * Curated, continuously updated.
  * Malware infrastructure, phishing domains, botnets, etc.
* **Custom TI Feeds:**
  * Upload your own threat data from open sources like AlienVault OTX, Abuse.ch, MISP, etc.
* **Taxii Server Integration:**
  * Pull threat feeds directly using TAXII protocol (Structured Threat Information Expression).

**Steps to Integrate TI:**

1. Microsoft Sentinel → **Threat Intelligence** → **Indicators**.
2. Click **+ Add Indicator** to manually upload (or automate ingestion).
3. Use Data Connectors like **Threat Intelligence Platforms** to automate feeds.

**TI Connectors to Know:**

| Connector                              | Use                                        |
| -------------------------------------- | ------------------------------------------ |
| Threat Intelligence Platforms          | Connect TAXII servers or third-party feeds |
| Microsoft Defender Threat Intelligence | Built-in TI from Microsoft                 |

***

### **Lesson 6.3: Managing Indicators of Compromise (IoCs)**

**Indicator Attributes:**

| Field                | Description                    |
| -------------------- | ------------------------------ |
| **Type**             | IP, URL, Domain, File Hash     |
| **Confidence Level** | High, Medium, Low              |
| **Threat Type**      | Malware, Phishing, Botnet      |
| **Source**           | Where the intel came from      |
| **Expiration**       | When the intel becomes invalid |

**Indicator Lifecycle:**

1. **Active:** Indicator is valid and in use.
2. **Expired:** Indicator is outdated (but remains in history).
3. **Revoked:** Indicator was found to be false or invalid.

**SOC Best Practice:**

* Focus on **high-confidence** and **recent** indicators.
* **Expire old indicators** to prevent noisy or invalid detections.

***

### **Lesson 6.4: Building TI-Driven Detections**

**Use TI in KQL Queries:**

**Example 1: IP Address Matching**

```kql
kqlCopyEditlet maliciousIPs = ThreatIntelligenceIndicator
| where Active == true and ExpirationDateTime > now()
| where IndicatorType == "ipv4"
| project NetworkIP = IndicatorValue;
SigninLogs
| where IPAddress in (maliciousIPs)
```

(Detect logins from known malicious IPs.)

***

**Example 2: Domain Matching**

```kql
kqlCopyEditlet maliciousDomains = ThreatIntelligenceIndicator
| where Active == true and ExpirationDateTime > now()
| where IndicatorType == "domain-name"
| project DomainName = IndicatorValue;
DeviceNetworkEvents
| where RemoteUrl in (maliciousDomains)
```

(Detect endpoints connecting to known phishing domains.)

***

**Example 3: URL Matching**

```kql
kqlCopyEditlet maliciousURLs = ThreatIntelligenceIndicator
| where Active == true and ExpirationDateTime > now()
| where IndicatorType == "url"
| project MaliciousURL = IndicatorValue;
CloudAppEvents
| where Url in (maliciousURLs)
```

(Monitor for users clicking on malicious links.)

***

### **Lesson 6.5: Automating TI Ingestion**

**Options to Automate Threat Feeds:**

* **Logic Apps:** Pull indicators daily from a public feed and inject into Sentinel.
* **TI Connectors:** Auto-sync using TAXII or custom APIs.
* **REST API:** Push your own threat intel using Sentinel’s API.

**Example Workflow:**

* Pull new indicators every 6 hours → Push to `ThreatIntelligenceIndicator` table → Detections run automatically against them.

> **Detection Engineering Tip:**\
> Automated threat intel enrichment increases your **detection speed** while reducing **manual effort**.
