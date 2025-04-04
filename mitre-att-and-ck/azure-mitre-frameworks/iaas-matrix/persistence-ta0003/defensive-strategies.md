# Defensive Strategies

## **Defensive Strategies Against Persistence in Azure Environments**

Persistence defense in Azure is about **locking down identity manipulation**, **protecting cloud infrastructure**, **hardening authentication pathways**, and **detecting unauthorized modifications**.

You want to **trap** attackers early, **restrict** persistence vectors, and **detect** any abnormal footholds quickly.

***

### 👤 Account Manipulation → Additional Cloud Credentials / Roles / SSH Authorized Keys

| Defensive Action                                                                                                                                             | Why It Matters                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| 🔒 Enforce Privileged Identity Management (PIM) and JIT activation for all privileged roles                                                                  | No standing privilege = harder to escalate or persist |
| 🚫 Disable permission to create additional credentials unless strictly necessary (Azure AD Role: Application Administrator, Cloud Application Administrator) | Stop hidden client secret additions                   |
| 📜 Use Defender for Cloud Identity Protection to monitor and alert on new credential or secret creation                                                      | Immediate detection of credential abuse               |
| 🛡️ Disable VM extensions after deployment (VMAccessForLinux, CustomScript) unless absolutely needed                                                         | Attackers can't plant SSH keys post-deployment        |
| 🔍 Monitor Azure Activity Logs and Sign-In Logs for new role assignments or SSH key modifications                                                            | Visibility into role or access tampering              |

✅ **Effect**: Attackers can't silently manipulate credentials or roles for persistence.

***

### 🛠️ Create Account → Cloud Account

| Defensive Action                                                                                               | Why It Matters                                      |
| -------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 📜 Enforce Access Reviews and entitlement management in Azure AD (Identity Governance)                         | Detect and remove rogue users or Service Principals |
| 🛡️ Apply Conditional Access policies to force MFA and compliant devices for all new users                     | No easy login paths for attacker-created accounts   |
| 🚫 Restrict who can create new users, SPNs, and B2B guest accounts using Azure RBAC                            | Only trusted admins can onboard identities          |
| 🔍 Alert on new Service Principal or user creation via Azure Activity Logs, Defender for Identity, or Sentinel | Detect account creation fast                        |

✅ **Effect**: Attackers can’t hide by creating new cloud identities easily.

***

### 📅 Event Triggered Execution

| Defensive Action                                                                                            | Why It Matters                                      |
| ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 🛡️ Apply Azure Policy to restrict who can create Logic Apps, Event Grid Subscriptions, and Azure Functions | No open event trigger deployments                   |
| 📜 Use Defender for Cloud to monitor for new Logic Apps or Function App deployments                         | Event-driven triggers can't be planted silently     |
| 🔍 Log and alert on Event Grid subscription creations and new function deployments                          | Watch for malicious event-driven persistence setups |

✅ **Effect**: No silent, auto-triggered attack chains inside Azure services.

***

### 🧬 Implant Internal Image

| Defensive Action                                                                           | Why It Matters                                |
| ------------------------------------------------------------------------------------------ | --------------------------------------------- |
| 📜 Enforce image signing policies (Azure Container Registry content trust, Cosign)         | Only signed, verified containers can run      |
| 🛡️ Scan all pushed container images in Azure Container Registry (Defender for Containers) | Detect backdoors or malware early             |
| 🚫 Restrict ACR push permissions with fine-grained Azure RBAC                              | Attackers can’t poison registries easily      |
| 🔍 Monitor ACR Push/Deploy events for unknown sources                                      | Alert on suspicious or rogue image activities |

✅ **Effect**: Malicious images can't be implanted into trusted registries and clusters.

***

### 🛡️ Modify Authentication Process → MFA, Hybrid Identity, Conditional Access

| Defensive Action                                                                                                            | Why It Matters                          |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| 🔒 Require MFA for all Azure AD privileged accounts — enforced by Conditional Access                                        | Block silent disablement of MFA         |
| 🚫 Lock down Azure AD Connect — allow access to AD Connect servers only from trusted admin workstations                     | Prevent hybrid identity persistence     |
| 📜 Review and restrict who can modify Conditional Access Policies (Azure AD roles like Global Admin, Security Admin only)   | Protect the auth enforcement mechanisms |
| 🔍 Audit Conditional Access Policy changes in Azure AD Logs and alert for risky modifications (e.g., exclusions, disabling) | Detect weakening of login protections   |

✅ **Effect**: Attackers can’t tamper with MFA, CA policies, or hybrid identity without triggering alerts.

***

### 👥 Valid Accounts → Default Accounts and Cloud Accounts

| Defensive Action                                                                                                        | Why It Matters                                 |
| ----------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 📜 Identify and disable unused or default accounts in Azure AD and subscriptions                                        | Reduce identity sprawl                         |
| 🛡️ Apply Smart Lockout policies and monitor for login anomalies (impossible travel, unfamiliar sign-ins)               | Stop credential reuse silently                 |
| 🚫 Use Conditional Access to restrict sign-ins to trusted devices/locations                                             | Further limit stolen account utility           |
| 🔍 Enable Identity Protection Risk Policies to auto-respond to risky sign-ins (force password reset, MFA re-enrollment) | Auto-defense against cloud account persistence |

✅ **Effect**: Stolen or leftover accounts become hard or impossible to persist with.

***

## 📊 Defensive Coverage Table (Persistence in Azure)

| Attack Vector                                     | Defensive Strategy                                                  |
| ------------------------------------------------- | ------------------------------------------------------------------- |
| Credential or role manipulation                   | PIM, JIT, Activity Logs, Defender alerts                            |
| Rogue cloud account creation                      | Access Reviews, restricted user creation rights                     |
| Event-driven persistence (Logic Apps, Event Grid) | Policy + Defender monitoring on new event triggers                  |
| Malicious container images                        | Content trust, image scanning, registry RBAC restrictions           |
| MFA/Hybrid Identity tampering                     | Conditional Access lockdown, AD Connect hardening                   |
| Abuse of default/cloud accounts                   | Disable defaults, enforce Smart Lockout, Identity Protection alerts |

***

## 🎯 Final Summary

Defending against Persistence in Azure focuses on:

* **Locking down identities and authentication systems** (MFA, CA Policies, Hybrid Identity)
* **Controlling credential and role manipulation tightly** (PIM, Defender, Activity Logs)
* **Hardening serverless and containerized platforms** (Image signing, restricted event triggers)
* **Detecting unauthorized account creations and changes fast** (Sentinel, Defender, Azure Logs)
