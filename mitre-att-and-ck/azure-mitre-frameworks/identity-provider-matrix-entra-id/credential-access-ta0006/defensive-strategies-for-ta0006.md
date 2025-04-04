# Defensive Strategies for TA0006

###

## **Defensive Strategies Against Credential Access in Entra ID**

Credential Access attacks are about **stealing, cracking, or forging credentials and tokens** to hijack identities.\
Defense focuses on **hardening authentication**, **protecting secrets**, and **detecting abuse early**.

***

### 🔓 Brute Force (Password Guessing, Cracking, Spraying, Credential Stuffing)

| Defensive Action                                                                              | Why It Matters                                 |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| 🔒 Enable Azure AD Smart Lockout and Password Protection (banned passwords list)              | Auto-block brute force and simple password use |
| 🚫 Enforce phishing-resistant MFA (FIDO2, Certificate-based, Smartcards) everywhere           | Make password theft useless                    |
| 📜 Monitor and alert on multiple failed sign-in attempts (Microsoft Sentinel)                 | Detect brute force and spray early             |
| 🛡️ Apply Conditional Access policies to block legacy protocols (e.g., POP, IMAP)             | Prevent bypassing modern auth protections      |
| 🔒 Implement Adaptive Risk-Based Conditional Access (block risky IPs and anomalous behaviors) | Auto-contain active attacks                    |

✅ **Effect**: Brute force becomes noisy and ineffective.

***

### 💥 Exploitation for Credential Access (T1212)

| Defensive Action                                                                                              | Why It Matters                  |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| 🔒 Secure Azure Functions, Logic Apps, and Storage Accounts with private endpoints and strong access controls | No public secrets exposure      |
| 🚫 Rotate secrets regularly for all services and applications                                                 | Reduce window of exposure       |
| 📜 Scan Azure environments for public access misconfigurations (Defender for Cloud, MS Purview)               | Catch exposed credentials early |

✅ **Effect**: No open paths to extract secrets.

***

### 🔏 Forge Web Credentials → SAML Tokens (Golden SAML, T1606.002)

| Defensive Action                                                                                   | Why It Matters                 |
| -------------------------------------------------------------------------------------------------- | ------------------------------ |
| 🔒 Protect SAML signing certificates in HSMs (Hardware Security Modules)                           | Prevent theft of key materials |
| 🚫 Enable automatic certificate rotation and expiry enforcement                                    | Minimize stolen cert reuse     |
| 📜 Monitor abnormal SAML authentication patterns (multiple SSO events without password validation) | Detect token forgery behavior  |
| 🛡️ Prefer Azure Entra ID native authentication (OIDC) over SAML where possible                    | Reduce SAML attack surface     |

✅ **Effect**: Golden SAML attacks become extremely hard.

***

### 🔄 Modify Authentication Process (MFA, Hybrid Identity, Conditional Access Policies)

| Defensive Action                                                                | Why It Matters                         |
| ------------------------------------------------------------------------------- | -------------------------------------- |
| 🔒 Lock MFA registration/reset (Authentication Methods Policy + Admin Approval) | Stop rogue MFA method takeovers        |
| 🚫 Require reauthentication for MFA method changes                              | Add friction to hijacking              |
| 📜 Monitor for MFA registration/reset events in logs                            | Detect stealthy MFA tampering          |
| 🔒 Secure Azure AD Connect (limit admins, monitor sync changes)                 | Stop hybrid identity manipulation      |
| 🚫 Require approval workflow for Conditional Access policy changes              | Protect strong authentication rules    |
| 📜 Alert on Conditional Access policy disables, edits, or exclusions            | Detect CA policy tampering immediately |

✅ **Effect**: Authentication paths stay hardened and visible.

***

### 🔄 MFA Request Generation (MFA Bombing, T1111)

| Defensive Action                                                      | Why It Matters             |
| --------------------------------------------------------------------- | -------------------------- |
| 🔒 Enable Number Matching for Microsoft Authenticator MFA prompts     | Stop approval fatigue      |
| 🚫 Train users on MFA fatigue/vishing attack patterns                 | Improve human resilience   |
| 📜 Monitor excessive MFA prompt generations (high volume MFA prompts) | Detect MFA bombing attacks |

✅ **Effect**: Users are hardened against MFA fatigue social engineering.

***

### 🔑 Steal Application Access Token (T1528)

| Defensive Action                                                                                     | Why It Matters                |
| ---------------------------------------------------------------------------------------------------- | ----------------------------- |
| 🔒 Shorten token lifetimes (access and refresh tokens)                                               | Limit session hijack time     |
| 🚫 Require Conditional Access evaluation even for active tokens (Continuous Access Evaluation - CAE) | Kill stolen tokens on-the-fly |
| 📜 Monitor anomalous token usage (same token from multiple IPs)                                      | Catch token theft attempts    |

✅ **Effect**: OAuth token abuse becomes difficult and short-lived.

***

### 🔏 Steal or Forge Authentication Certificates (T1649)

| Defensive Action                                                                     | Why It Matters          |
| ------------------------------------------------------------------------------------ | ----------------------- |
| 🔒 Store all certificates in secured Azure Key Vaults with RBAC and Purge Protection | Stop cert theft         |
| 🚫 Enable monitoring and alerts on key export events in Azure Key Vault              | Catch cert exfiltration |
| 📜 Rotate authentication certificates regularly                                      | Minimize risk window    |

✅ **Effect**: Authentication certificates are protected against theft and misuse.

***

### 🔓 Unsecured Credentials (T1552)

| Defensive Action                                                                                       | Why It Matters                   |
| ------------------------------------------------------------------------------------------------------ | -------------------------------- |
| 🔒 Audit public storage, GitHub, and Azure DevOps repositories regularly                               | Find leaked secrets              |
| 🚫 Enforce secret scanning in DevOps pipelines (e.g., GitHub Advanced Security, Azure DevOps policies) | Prevent secret leakage           |
| 📜 Alert on storage account changes (new public containers)                                            | Detect new exposures immediately |

✅ **Effect**: Credentials don't leak quietly.

***

## 📊 **Defensive Coverage Table (Credential Access in Entra ID)**

| Attack Vector                                        | Defensive Strategy                                           |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| Brute Force (Guessing, Spraying, Cracking, Stuffing) | MFA, smart lockout, risk-based blocking                      |
| Exploitation for Credential Access                   | Secure cloud resources, scan for exposed secrets             |
| Golden SAML (Forge SAML Tokens)                      | Protect SAML certs, monitor SSO behaviors                    |
| Modify Authentication Process (MFA, Hybrid, CA)      | Secure MFA reset, hybrid sync monitoring, CA edit protection |
| MFA Request Generation (MFA Bombing)                 | Number Matching, user training, MFA prompt monitoring        |
| Steal Application Access Token                       | Short token life, CAE enforcement, token behavior monitoring |
| Steal or Forge Authentication Certificates           | Secure cert storage, audit key operations, cert rotation     |
| Unsecured Credentials                                | Scan public repos, enforce secret scanning policies          |

***

## 🎯 Final Summary

Defending against Credential Access in Entra ID focuses on:

* **Making password and token theft ineffective**
* **Hardening authentication workflows and secrets management**
* **Detecting credential abuse and suspicious authentications early**
