# Defensive Strategies

## **Defensive Strategies Against Defense Evasion in Azure Environments**

In Azure, defending against Defense Evasion means **locking down configuration changes**, **monitoring credential usage**, **protecting logging and monitoring**, and **detecting manipulation of authentication paths**.\
If you stop evasion, you expose attackers **early**.

***

### ⬆️ Abuse Elevation Control Mechanism → Temporary Elevated Cloud Access (T1548)

| Defensive Action                                                                   | Why It Matters                      |
| ---------------------------------------------------------------------------------- | ----------------------------------- |
| 🔒 Require multi-party approval for PIM JIT activations (Azure PIM)                | Attackers can’t easily self-elevate |
| 🚫 Monitor PIM role activation logs using Azure Monitor                            | Detect unusual elevation attempts   |
| 📜 Use Conditional Access with strict device compliance and MFA for JIT activation | Force secure context for elevation  |

✅ **Effect**: Lock down temporary escalations used to bypass protections.

***

### ⚡ Exploitation for Defense Evasion (T1211)

| Defensive Action                                                                              | Why It Matters                         |
| --------------------------------------------------------------------------------------------- | -------------------------------------- |
| 🛡️ Enable Defender for Cloud recommendations and remediate all critical misconfigurations    | Close holes that allow silent bypasses |
| 📜 Regularly scan Azure environment with Defender and external CSPM tools (e.g., Wiz, Prisma) | Surface hidden misconfigurations early |
| 🔍 Monitor for "atypical permissions granted" via Azure Activity Logs                         | Detect exploit chains early            |

✅ **Effect**: No easy exploitation paths left for attackers.

***

### 🛡️ Impair Defenses (Disable or Modify Tools / Firewall / Logs)

| Defensive Action                                                                                              | Why It Matters                            |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| 🔒 Apply Azure Policy to **enforce** monitoring agent presence (Defender agents, Log Analytics)               | Mandatory security tooling                |
| 🚫 Block role assignment for disabling Defender settings to only security administrators                      | Attackers can’t easily disable monitoring |
| 📜 Use Azure Activity Log alerts for security settings changes (e.g., WAF config updates, NSG rule deletions) | Catch firewall and tooling tampering fast |
| 🔍 Monitor Diagnostic Settings deletions and alert immediately                                                | Broken log pipelines = immediate red flag |

✅ **Effect**: Attackers can't turn off your eyes and ears.

***

### 🔒 Modify Authentication Process (MFA / Hybrid Identity / Conditional Access Policies)

| Defensive Action                                                                        | Why It Matters                                   |
| --------------------------------------------------------------------------------------- | ------------------------------------------------ |
| 🔒 Require MFA and device compliance for **every** privileged user (Conditional Access) | Prevent silent login manipulation                |
| 🚫 Protect Azure AD Connect sync servers with network and privileged access controls    | Hybrid identity protected                        |
| 📜 Enable audit logging for Conditional Access policy changes                           | Detect tampering with authentication protections |
| 🔍 Monitor for new trusted locations/IP ranges added to Conditional Access policies     | Silent bypasses caught fast                      |

✅ **Effect**: Identity flows stay hardened even if attackers try to erode protections.

***

### 🖥️ Modify Cloud Compute Infrastructure (Snapshots, Cloning, Deletion, Revert)

| Defensive Action                                                                             | Why It Matters                       |
| -------------------------------------------------------------------------------------------- | ------------------------------------ |
| 🔒 Apply Azure Policies to control who can create, attach, or revert snapshots               | No rogue clones                      |
| 🚫 Require approvals for VM deletions (Azure Blueprints, Policy + Approval gates)            | Prevent evidence destruction         |
| 📜 Monitor snapshot creation, attachment, and deletion events                                | Alert on stealth snapshot activities |
| 🔍 Enable Defender for Cloud file integrity monitoring (Azure Monitor Agent) on critical VMs | Catch unauthorized revert operations |

✅ **Effect**: Compute manipulations for hiding activities are detected immediately.

***

### 🏢 Modify Cloud Resource Hierarchy

| Defensive Action                                                                                                   | Why It Matters                      |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------- |
| 🔒 Lock down who can modify Azure Management Groups and Subscription hierarchy (Management Group Contributor only) | No hidden management group creation |
| 📜 Monitor management group changes via Azure Activity Logs                                                        | Alert when hierarchy changes occur  |

✅ **Effect**: Attackers can't hide infrastructure changes under your nose.

***

### 🌎 Unused/Unsupported Cloud Regions

| Defensive Action                                                      | Why It Matters                    |
| --------------------------------------------------------------------- | --------------------------------- |
| 🔒 Restrict deployments to approved Azure regions via Azure Policy    | No deployments in obscure regions |
| 📜 Monitor deployments in unsupported regions with Defender for Cloud | Catch out-of-bound region usage   |

✅ **Effect**: Force attackers to operate where you're watching.

***

### 🛡️ Use Alternate Authentication Material (Tokens, Cookies)

| Defensive Action                                                                                                   | Why It Matters                    |
| ------------------------------------------------------------------------------------------------------------------ | --------------------------------- |
| 🔒 Rotate service principal secrets regularly and minimize token lifetimes (Workload Identity, short-lived tokens) | Tokens can't stay valid forever   |
| 🚫 Restrict token access in workloads by setting `automountServiceAccountToken: false` in Kubernetes               | Harder to steal tokens at runtime |
| 📜 Enable Defender for Cloud to monitor suspicious access token use                                                | Detect token theft                |
| 🔍 Monitor abnormal session cookie usage (via Azure AD Sign-In Logs)                                               | Detect console hijacks            |

✅ **Effect**: Even if tokens are stolen, detection and invalidation are rapid.

***

### 👥 Valid Accounts (Default Accounts / Cloud Accounts)

| Defensive Action                                                                                   | Why It Matters                                 |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 🔒 Identify, monitor, and rotate credentials for default service principals and managed identities | No "free" persistence                          |
| 🚫 Apply Identity Protection Risk Policies (auto-disable risky accounts)                           | Stolen cloud accounts can’t be reused silently |
| 📜 Require Privileged Identity Management (PIM) for high-privileged cloud accounts                 | Temporary roles, no standing privilege         |

✅ **Effect**: Cloud accounts can't be abused for hiding operations.

***

## 📊 **Defensive Coverage Table (Defense Evasion in Azure)**

| Attack Vector                                                | Defensive Strategy                                              |
| ------------------------------------------------------------ | --------------------------------------------------------------- |
| Temporary Elevated Cloud Access                              | PIM approvals, role monitoring, CA enforcement                  |
| Exploitation for Defense Evasion                             | Defender for Cloud misconfig scanning, Azure Policy enforcement |
| Disable or Modify Tools/Firewall/Logs                        | Monitor config changes, mandatory agents, activity alerts       |
| Modify Authentication (MFA, CA, Hybrid)                      | Harden CA policies, audit logs, secure hybrid identity          |
| Modify Compute Infrastructure (Snapshots, Cloning, Deletion) | Approvals for snapshot use, deletion monitoring                 |
| Modify Cloud Resource Hierarchy                              | Lock hierarchy changes, monitor management group updates        |
| Deploy in Unsupported Regions                                | Azure Policy restrictions, Defender for Cloud alerts            |
| Use Alternate Authentication Material                        | Token rotation, session cookie monitoring                       |
| Abuse Default/Cloud Accounts                                 | Identity Protection Risk Policies, PIM enforcement              |

***

## 🎯 Final Summary

Defending against Defense Evasion in Azure focuses on:

* **Locking down privilege escalation paths and security setting changes**
* **Protecting logs, monitoring agents, and detection infrastructure**
* **Hardening authentication flows against tampering**
* **Detecting token, cookie, and credential theft early**
* **Restricting deployments to known and monitored regions**
