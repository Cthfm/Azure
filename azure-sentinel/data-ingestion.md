---
hidden: true
---

# Data Ingestion

### **Built-in Connectors Overview**

**Microsoft Sentinel** offers over **150+ built-in data connectors** to easily pull logs from:

| Source Type             | Examples                                                           |
| ----------------------- | ------------------------------------------------------------------ |
| **Microsoft**           | Azure AD, Office 365, Defender for Endpoint, Defender for Identity |
| **Third-Party Clouds**  | AWS, GCP                                                           |
| **On-Premises**         | Firewalls (Palo Alto, Fortinet), Syslog, Windows Servers           |
| **Custom Applications** | REST API, Common Event Format (CEF) collectors                     |

**Connectors** automatically normalize data into a standard schema.

> **SOC Tip:** Start with _Microsoft-native_ connectors first for quick wins (Azure AD, Office 365, Defender).

***

### **Lesson 3.2: Connecting Azure Data Sources**

**Critical Azure Services to Connect:**

* **Azure AD:** User sign-ins, risky logins
* **Azure Activity:** Resource modifications, deployments
* **Key Vault Logs:** Secrets access
* **Azure Firewall Logs:** Inbound/outbound traffic
* **Microsoft Defender for Cloud:** Threat alerts across Azure resources

**Steps to Connect Azure Sources:**

1. Microsoft Sentinel → **Configuration** → **Data connectors**.
2. Search for the service (e.g., Azure Active Directory).
3. Click the connector → **Open Connector Page** → **Connect**.
4. Select your subscriptions/tenants/workspaces as needed.

**Permissions Needed:**\
You need at least **Contributor** rights on the Azure resource to connect it.

> **Incident Response Tip:**\
> Azure Activity and SigninLogs are _must-haves_ for any credible incident investigation.

***

### **Lesson 3.3: Connecting Microsoft 365**

**Key Microsoft 365 Sources:**

* **Office 365 Exchange:** Email activity (send, receive, read)
* **Office 365 SharePoint:** File access and sharing
* **Microsoft Teams:** Messaging events
* **Defender for Endpoint:** Endpoint alerts and telemetry
* **Defender for Identity:** Domain controller activity

**Steps to Connect:**

1. Microsoft Sentinel → **Data connectors**.
2. Search for "Office 365" or "Microsoft 365 Defender".
3. Connect each workload (Exchange, SharePoint, Teams).

**Behind the Scenes:**\
Office 365 logs pull from the **Unified Audit Log (UAL)** in Microsoft 365.

**Common Tables Created:**

* `OfficeActivity`
* `EmailEvents`
* `DeviceEvents`
* `IdentityInfo`

> **SOC Tip:** EmailEvents and DeviceEvents tables are _gold mines_ during phishing and malware investigations.

***

### **Lesson 3.4: Connecting On-Premises Data (Syslog, CEF, Windows Servers)**

You often need to connect:

* **Firewalls**
* **IDS/IPS systems**
* **On-prem Windows servers**

**Options:**

* **Syslog Connector:** Standard for Linux devices, firewalls
* **CEF Connector:** Structured log format for security devices
* **Windows Security Events Connector:** Collect event logs via the Microsoft Monitoring Agent (MMA)

**How Syslog and CEF Work:**

* Install the **Log Analytics Agent** (or use the newer Azure Monitor Agent).
* Configure the agent to forward Syslog or CEF logs to the Log Analytics workspace.

**Supported Facilities/Severities for Syslog:**

* auth, authpriv, daemon, user, local0-local7, etc.

> **Detection Engineering Tip:**\
> Critical events like "Authentication Failure" (`EventID 4625`) and "New Service Installed" (`EventID 7045`) should be forwarded from Windows servers.

***

### **Lesson 3.5: AWS and GCP Integration**

**AWS Integration:**

* Use the **AWS CloudTrail Connector** to ingest:
  * Management events
  * S3 access logs
  * IAM activity
* Requires setting up an S3 bucket and SNS topic for event forwarding.

**GCP Integration:**

* Use **Google Cloud Platform (GCP) connector**.
* Ingest:
  * Admin Activity
  * Data Access logs
  * System Events

**Authentication:**\
Set up an app registration (Service Principal) or use a Service Account (for GCP).

> **SOC Tip:** CloudTrail events are **essential** for catching privilege escalation or unauthorized access in AWS environments.
