# Defensive Strategies

## **Defensive Strategies Against Initial Access in Azure Environments**

In Azure, defending against Initial Access involves **reducing the external attack surface**, **securing identities**, **hardening trusted connections**, and **detecting abuse attempts** early.

You must **close off entry points** _before_ adversaries land.

***

### 🌐 Exploit Public-Facing Application (T1190)

| Defensive Action                                                                                           | Why It Matters                                                          |
| ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| 📜 Enable Azure Web Application Firewall (WAF) in front of all Azure App Services and APIs                 | Block common exploits like SQLi, XSS, RCE automatically                 |
| 🔒 Regularly scan public endpoints with Defender for Cloud, Qualys, or Nessus                              | Identify vulnerabilities before attackers do                            |
| 🚫 Restrict Azure App Service Public Access: Require authentication (Azure Front Door, Azure AD App Proxy) | Prevent unauthenticated public access to apps                           |
| 🔍 Monitor for abnormal access patterns in App Insights and Defender for App Services                      | Detect exploit attempts (e.g., spikes in POSTs to unexpected endpoints) |
| 📦 Keep AKS clusters updated and apply security patches automatically (Azure Patch Management)             | Protect Kubernetes workloads                                            |

✅ **Effect**: Reduces the likelihood of successful exploitation of publicly exposed Azure services.

***

### 🔗 Trusted Relationship (T1199)

| Defensive Action                                                                             | Why It Matters                                       |
| -------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| 🔒 Use Azure AD Cross-Tenant Access Settings to restrict B2B access (trust but verify model) | Only allow specific, verified tenants limited access |
| 📜 Review all guest users in Azure AD regularly (Azure AD Access Reviews)                    | Remove stale or risky external accounts              |
| 🛡️ Enforce MFA (Multi-Factor Authentication) and Conditional Access for B2B users           | Reduce risk if external identities are compromised   |
| 🚫 Never assign Contributor, Owner, or User Access Administrator roles to guest users        | Principle of least privilege across tenants          |
| 🔍 Monitor cross-tenant access logs using Azure AD Sign-In Logs                              | Detect abnormal external access activity early       |

✅ **Effect**: Strongly controls abuse of external trusted identities and cross-tenant compromises.

***

### 👤 Valid Accounts → Default Accounts

| Defensive Action                                                                                 | Why It Matters                               |
| ------------------------------------------------------------------------------------------------ | -------------------------------------------- |
| 🔒 Disable or remove default credentials immediately on service principals, VMs, databases       | Defaults are the easiest targets             |
| 📜 Rotate client secrets and certificates for all Service Principals every 90 days (minimum)     | Short-lived secrets minimize impact of leaks |
| 🛡️ Use Managed Identities instead of hardcoded secrets when possible (identity without secret)  | Reduces static secret exposure entirely      |
| 🚫 Apply Azure Policy to deny creation of service principals without expiration on secrets       | Force rotation discipline across the org     |
| 🔍 Enable Defender for Cloud App Control alerts on high-privilege SPNs (Service Principal Names) | Detect risky service principal behavior      |

✅ **Effect**: Prevents attackers from easily using old, static, or default credentials in your Azure environment.

***

### ☁️ Valid Accounts → Cloud Accounts

| Defensive Action                                                                                                       | Why It Matters                                           |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| 🔒 Enforce Conditional Access policies for cloud accounts (block legacy auth, require MFA, device compliance)          | Makes it harder to abuse stolen credentials              |
| 📜 Enable Identity Protection Risk Policies to auto-respond to risky logins (e.g., password spray, impossible travel)  | Detect credential compromise in real time                |
| 🛡️ Require privileged Azure AD accounts to use Privileged Identity Management (PIM) with Just-In-Time (JIT) elevation | Reduces exposure of standing admin accounts              |
| 🚫 Disable unused accounts and enforce account lockout after repeated failed attempts (Smart Lockout)                  | Shrink attack surface of valid but unused cloud accounts |
| 🔍 Monitor Azure AD Sign-In Logs and enable Microsoft Sentinel queries for impossible travel, risky sign-ins           | High-fidelity alerts on stolen credentials use           |

✅ **Effect**: Strongly hardens cloud account usage and identity protection, stopping stolen credential abuse.

***

## 📊 Defensive Coverage Table (Initial Access in Azure)

| Attack Vector             | Defensive Strategy                                                                  |
| ------------------------- | ----------------------------------------------------------------------------------- |
| Exploit Public-Facing App | WAF, Patch Management, App Service Authentication, Defender alerts                  |
| Trusted Relationship      | Cross-Tenant Access Settings, MFA for B2B, guest user cleanup                       |
| Valid Accounts (Default)  | Disable defaults, rotate secrets, use Managed Identities, policy enforcement        |
| Valid Accounts (Cloud)    | Conditional Access, PIM for privileged users, lockout policies, Identity Protection |

***

## 🎯 Final Summary

Defending against Initial Access in Azure focuses on:

* **Reducing public attack surface** (App Services, APIs, AKS hardening)
* **Controlling trusted external user access** (B2B, federation lockdowns)
* **Securing default credentials and Service Principals** (rotation + enforcement)
* **Hardening cloud account authentication** (MFA, Conditional Access, Identity Protection)
