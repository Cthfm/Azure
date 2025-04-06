# Microsoft Graph Security API

## **What is the Microsoft Graph Security API?**

The **Microsoft Graph Security API** is a **unified endpoint** that aggregates security information from across Microsoft 365 services, such as:

* Microsoft Defender for Endpoint
* Microsoft Defender for Identity
* Microsoft Defender for Office 365
* Microsoft Cloud App Security (MCAS)
* Azure Active Directory Identity Protection

Instead of querying each service separately, you can get **all security alerts in one place**.

👉 Endpoint:

```
bashCopyEdithttps://graph.microsoft.com/v1.0/security/
```

***

## 🧩 **Key Security API Resources**

| Resource                               | Purpose                                                                      |
| -------------------------------------- | ---------------------------------------------------------------------------- |
| `/security/alerts`                     | Access alerts like malware detections, risky logins, phishing attempts, etc. |
| `/security/incidents`                  | Group related alerts into incidents for easier management.                   |
| `/security/secureScores`               | Measure how secure your organization is.                                     |
| `/security/secureScoreControlProfiles` | Review recommendations to improve security.                                  |

***

## 🚨 **Why Use the Security API?**

✅ **Centralize security data** across multiple services.\
✅ **Automate security investigations** by pulling alerts into your own systems (SIEMs, SOARs).\
✅ **Trigger response actions** based on alert severity.\
✅ **Monitor your organization's Secure Score** and drive security improvements.

***

## 🛠️ **Permissions Needed for Security API**

To access the Security API, your app needs one or more of these permissions:

| Permission                      | Purpose                                        |
| ------------------------------- | ---------------------------------------------- |
| `SecurityEvents.Read.All`       | Read security alerts and incidents.            |
| `SecurityEvents.ReadWrite.All`  | Read and update security alerts and incidents. |
| `SecurityActions.ReadWrite.All` | Take response actions (e.g., block accounts).  |

🔔 **Important:**\
These permissions are **highly privileged** and **require admin consent**.

***

## 🛠️ **Working with Security Alerts**

***

#### 🧠 1. Get All Security Alerts

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/alerts
Authorization: Bearer {access_token}
```

✅ Retrieves **all active alerts** in your organization.

***

#### 🧠 2. Filter Alerts by Severity

Only get critical alerts:

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/alerts?$filter=severity eq 'high'
```

✅ Useful for **prioritizing** incidents in a large environment.

***

#### 🧠 3. Get a Specific Alert

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/alerts/{alert-id}
```

✅ Retrieve full details about a specific alert.

***

#### 🧠 4. Update an Alert

Mark an alert as resolved:

```http
httpCopyEditPATCH https://graph.microsoft.com/v1.0/security/alerts/{alert-id}
Content-Type: application/json

{
  "status": "resolved",
  "feedback": "truePositive"
}
```

✅ You can **update status**, **assign owners**, and **add comments** for better tracking.

***

## 🛠️ **Working with Incidents**

***

#### 🧠 1. Get All Incidents

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/incidents
```

✅ Shows incidents, which are **groups of related alerts**.

***

#### 🧠 2. Get Alerts in an Incident

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/incidents/{incident-id}/alerts
```

✅ Lists all alerts tied to a particular incident.

***

## 📈 **Working with Secure Score**

The Secure Score API helps you **measure and track** your organization's security posture.

***

#### 🧠 1. Get Secure Scores

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/secureScores
```

✅ Pulls your organization's overall Secure Score history.

***

#### 🧠 2. Get Secure Score Improvement Actions

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/security/secureScoreControlProfiles
```

✅ Lists recommended actions to **improve your security** (e.g., enforce MFA, reduce admin privileges).

***

## 🛡️ **Best Practices When Using the Security API**

| Practice                          | Why It Matters                   | Tip                                                       |
| --------------------------------- | -------------------------------- | --------------------------------------------------------- |
| **Automate alert triage**         | Respond faster to threats.       | Pull high-severity alerts into your SIEM automatically.   |
| **Prioritize critical incidents** | Focus on what's most dangerous.  | Filter by `severity eq 'high'` or `status eq 'newAlert'`. |
| **Update alert statuses**         | Keep your environment clean.     | Resolve false positives and track real incidents.         |
| **Secure your app**               | Protect sensitive security data. | Use Conditional Access, least privilege, and log access.  |
