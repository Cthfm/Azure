# Defensive Strategies

## **Defensive Strategies Against Credential Access in Azure Environments**

In Azure, defending against Credential Access means **hardening authentication pathways**, **securing secrets**, **protecting access tokens**, and **detecting brute-force patterns** early.\
You want to **close every door** attackers can squeeze through.

***

### 🔑 Brute Force → Password Guessing, Password Spraying, Credential Stuffing (T1110.001, T1110.003, T1110.004)

| Defensive Action                                                                       | Why It Matters                                      |
| -------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 🔒 Enforce password protection policies via Azure AD Identity Protection               | Prevent weak passwords at account creation          |
| 🚫 Enable Smart Lockout and Risky Sign-In policies                                     | Block accounts after repeated failed login attempts |
| 📜 Monitor login anomalies like multiple failures, impossible travel via Azure AD logs | Detect brute force and stuffing fast                |
| 🛡️ Require MFA for **all** users, especially privileged users (Conditional Access)    | Even if password guessed, access still blocked      |

✅ **Effect**: Stop password-based attacks before they gain a foothold.

***

### 🔐 Credentials from Password Stores → Cloud Secrets Management (T1555.004)

| Defensive Action                                                                    | Why It Matters                                     |
| ----------------------------------------------------------------------------------- | -------------------------------------------------- |
| 🔒 Restrict Azure Key Vault access to minimum necessary identities using RBAC       | Only trusted apps and users can access secrets     |
| 🚫 Enable Key Vault logging (Diagnostic Settings) and alert on secret access events | Monitor who accesses sensitive secrets             |
| 📜 Rotate secrets and certificates regularly (use Key Vault auto-rotation)          | Reduce the window of stolen secret usefulness      |
| 🛡️ Enable soft-delete and purge protection on Key Vaults                           | Prevent attackers from deleting secrets stealthily |

✅ **Effect**: Attackers can't silently extract secrets without triggering alarms.

***

### 🛠️ Forge Web Credentials → Web Cookies and SAML Tokens (T1606.003, T1606.002)

| Defensive Action                                                                                          | Why It Matters                          |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| 🔒 Shorten Azure Portal session timeouts and require reauthentication for privileged operations           | Limit session hijack window             |
| 🚫 Use Conditional Access policies enforcing reauthentication based on risk signals (e.g., device change) | Detect stolen cookie usage              |
| 📜 Monitor Azure AD Sign-In logs for anomalous sessions (device ID, IP mismatch)                          | Catch forged or hijacked sessions early |
| 🛡️ Use Identity Protection Risk Policies (Azure AD) to block high-risk session activities                | Stop Golden SAML-based lateral movement |

✅ **Effect**: Hardens session security and detects impersonation attacks.

***

### 🛡️ Modify Authentication Process (MFA, Hybrid Identity, Conditional Access Policies) (T1556.006, T1556.007, T1556.008)

| Defensive Action                                                                                      | Why It Matters                                          |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| 🔒 Enforce MFA for **ALL** users, not just admins                                                     | Prevent silent logins even if credentials are stolen    |
| 🚫 Lock Conditional Access policy editing to a minimum set of administrators (Privileged Role Admins) | Prevent silent policy tampering                         |
| 📜 Enable audit logging for Conditional Access changes and alert on edits                             | Immediate detection of authentication process tampering |
| 🛡️ Harden Azure AD Connect configurations and restrict sync permissions                              | Secure hybrid identity from abuse                       |

✅ **Effect**: Authentication defenses stay hardened even against internal tampering.

***

### 🔔 MFA Request Generation (MFA Fatigue Attacks) (T1111)

| Defensive Action                                                            | Why It Matters                           |
| --------------------------------------------------------------------------- | ---------------------------------------- |
| 🔒 Use Number Matching or Passwordless Sign-in with Microsoft Authenticator | Prevent auto-approvals under pressure    |
| 🚫 Train users about MFA fatigue and phishing attacks                       | Reduce likelihood of accidental approval |
| 📜 Monitor for multiple MFA prompt failures in Azure AD logs                | Detect active MFA attack attempts        |

✅ **Effect**: Attackers can't trick users into approving malicious login requests easily.

***

### 🌐 Network Sniffing (T1040)

| Defensive Action                                                                                                          | Why It Matters                          |
| ------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| 🔒 Apply strict NSG (Network Security Group) rules to VMs and subnets                                                     | No promiscuous traffic sniffing allowed |
| 🚫 Encrypt all traffic (TLS 1.2/1.3) within Azure Virtual Networks using Application Gateway, Front Door, or Private Link | No cleartext to sniff                   |
| 📜 Monitor VM NIC settings for unusual packet captures or mirror settings                                                 | Catch sniffer setups early              |

✅ **Effect**: Attackers can't harvest credentials off network traffic.

***

### 🛡️ Steal Application Access Token (T1528)

| Defensive Action                                                                     | Why It Matters              |
| ------------------------------------------------------------------------------------ | --------------------------- |
| 🔒 Use Managed Identity token restrictions (limit scope, rotate tokens)              | Tokens stay short-lived     |
| 🚫 Disable automountServiceAccountToken for Kubernetes pods unless necessary         | Limit token exposure in AKS |
| 📜 Monitor for token usage anomalies (e.g., new source IPs) using Defender for Cloud | Catch token misuse early    |

✅ **Effect**: Even if tokens are stolen, detection and invalidation are fast.

***

### 🔓 Unsecured Credentials (Credentials In Files and Cloud Instance Metadata API) (T1552.001, T1552.005)

| Defensive Action                                                                                             | Why It Matters                          |
| ------------------------------------------------------------------------------------------------------------ | --------------------------------------- |
| 🔒 Use GitHub secret scanning and Azure DevOps secret scanning to catch leaked credentials                   | Block leak paths early                  |
| 🚫 Harden access to Azure VM metadata services with network controls and use Managed Identity best practices | Limit attacker access to IMDS endpoints |
| 📜 Monitor for unusual metadata service access patterns (e.g., curl to IMDS from VMs)                        | Alert on credential harvesting attempts |

✅ **Effect**: Protects against accidental or targeted credential harvesting.

***

## 📊 **Defensive Coverage Table (Credential Access in Azure)**

| Attack Vector                            | Defensive Strategy                                           |
| ---------------------------------------- | ------------------------------------------------------------ |
| Brute Force (Guessing/Spraying/Stuffing) | Enforce password policies, Smart Lockout, MFA everywhere     |
| Credentials from Password Stores         | Harden Key Vault access, enable secret access logging        |
| Forge Web Credentials (Cookies/SAML)     | Harden session timeouts, risk-based reauthentication         |
| Modify Authentication (MFA, CA, Hybrid)  | Lock policy editing, audit CA changes                        |
| MFA Request Generation                   | Use Number Matching MFA, train users, detect push fatigue    |
| Network Sniffing                         | Strict NSGs, TLS encryption, monitor VM NIC settings         |
| Steal Application Access Token           | Restrict token scope, monitor usage, block exposure          |
| Unsecured Credentials                    | Secret scanning, IMDS hardening, monitor for metadata access |

***

## 🎯 Final Summary

Defending against Credential Access in Azure focuses on:

* **Hardening identity verification** (MFA, CA Policies, Identity Protection)
* **Securing secrets and tokens across cloud services** (Key Vault, Managed Identities)
* **Protecting authentication material from harvesting** (sessions, tokens, passwords)
* **Detecting credential theft and brute-force patterns early**
