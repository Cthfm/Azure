# Defensive Strategies: TA0001

## **Defensive Strategies Against Initial Access in Entra ID (Azure Identity Environments)**

Defending against Initial Access in Entra ID means **blocking credential theft**, **securing authentication processes**, **harden trust relationships**, and **detecting abuse early**.

Identity is the first battlefield — **no foothold, no breach**.

***

### 🎯 Drive-by Compromise (T1189)

| Defensive Action                                                                | Why It Matters                                                  |
| ------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| 🔒 Enable OAuth Consent Governance in Entra ID                                  | Require admin approval for app consent to sensitive permissions |
| 🚫 Restrict user consent to verified publishers only (Consent Settings)         | Block rogue app consent phishing                                |
| 📜 Monitor risky OAuth applications in Microsoft Defender for Cloud Apps (MCAS) | Detect and investigate unauthorized app grants                  |
| 🛡️ Apply Conditional Access policies requiring MFA before app consent          | Add friction to consent phishing attacks                        |

✅ **Effect**: Stops drive-by OAuth attacks before they can steal tokens.

***

### 🎣 Phishing (Spearphishing Link, Spearphishing Voice)

***

#### ➡️ **Spearphishing Link (T1566.002)**

| Defensive Action                                                                     | Why It Matters                                             |
| ------------------------------------------------------------------------------------ | ---------------------------------------------------------- |
| 🔒 Enforce phishing-resistant MFA (FIDO2, Certificate-based Authentication)          | Credentials alone are not enough                           |
| 🚫 Enable Azure AD Identity Protection risky sign-in policies                        | Auto-block logins from unfamiliar IPs or sign-in anomalies |
| 📜 Deploy Defender for Office 365 anti-phishing and Safe Links protection            | Detect and rewrite malicious links in emails               |
| 🛡️ Enable Conditional Access policies to block sign-ins from risky or anonymous IPs | Cut off sessions coming from suspicious sources            |

✅ **Effect**: Email and credential phishing becomes far less effective.

***

#### ➡️ **Spearphishing Voice (Vishing) (T1566.004)**

| Defensive Action                                                                                 | Why It Matters                                  |
| ------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| 🔒 Implement Number Matching for Microsoft Authenticator MFA requests                            | Prevent users from approving random MFA prompts |
| 🚫 Train users on MFA fatigue/vishing attacks regularly (user awareness)                         | Lower success rate of social engineering        |
| 📜 Monitor multiple MFA prompt failures via Azure AD Sign-In Logs                                | Detect MFA fatigue attacks in real-time         |
| 🛡️ Apply high-risk sign-in Conditional Access policies (challenge or block risky MFA approvals) | Auto-block suspicious authentication attempts   |

✅ **Effect**: Vishing attacks fail because MFA approvals are user-verified.

***

### 🔗 Trusted Relationship (T1199)

| Defensive Action                                                                                     | Why It Matters                        |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------- |
| 🔒 Limit external collaboration settings (only invited, verified domains)                            | Restrict who can join your tenant     |
| 🚫 Enforce guest user access reviews and time-bound access                                           | Remove stale external accounts        |
| 📜 Monitor B2B user activities and risky sign-ins via Entra ID logs and Identity Protection          | Detect external account abuse         |
| 🛡️ Apply Conditional Access policies enforcing stricter rules on external users (e.g., require MFA) | Secure external identities separately |

✅ **Effect**: Cross-tenant abuse becomes difficult without detection.

***

### 👤 Valid Accounts (Default Accounts, Cloud Accounts)

***

#### ➡️ **Default Accounts (T1078.004)**

| Defensive Action                                                                                 | Why It Matters             |
| ------------------------------------------------------------------------------------------------ | -------------------------- |
| 🔒 Regularly audit and disable unused guest, service principal, and managed identity accounts    | Shrink attack surface      |
| 🚫 Apply least privilege to service principals and automation accounts                           | Minimize blast radius      |
| 📜 Enable Identity Protection policies to auto-disable risky accounts (e.g., leaked credentials) | Stop compromised defaults  |
| 🛡️ Rotate credentials for service principals regularly, use Managed Identity whenever possible  | Eliminate credential leaks |

✅ **Effect**: Default identities aren't low-hanging fruit anymore.

***

#### ➡️ **Cloud Accounts (T1078.004)**

| Defensive Action                                                                                    | Why It Matters                 |
| --------------------------------------------------------------------------------------------------- | ------------------------------ |
| 🔒 Apply Conditional Access policies enforcing MFA and compliant devices for all users              | Block unauthorized logins      |
| 🚫 Use risk-based Conditional Access to block high-risk users automatically                         | Stop compromised accounts      |
| 📜 Monitor sign-ins by geolocation, impossible travel, and risky IP detection (Identity Protection) | Catch credential theft fast    |
| 🛡️ Enable continuous access evaluation (CAE) to kill stolen sessions immediately                   | Real-time session invalidation |

✅ **Effect**: Stolen cloud credentials are useless without a trusted device or secondary authentication.

***

## 📊 **Defensive Coverage Table (Initial Access in Entra ID)**

| Attack Vector                 | Defensive Strategy                                                                  |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| Drive-by Compromise           | Consent Governance, Safe App Consent, risky OAuth app monitoring                    |
| Spearphishing Link            | Phishing-resistant MFA, Defender for Office 365 Safe Links, risky sign-in detection |
| Spearphishing Voice (Vishing) | Number Matching MFA, user training, risky MFA prompt detection                      |
| Trusted Relationship          | Limit external collaboration, enforce guest reviews, CA policies on guests          |
| Default Accounts              | Audit and clean up defaults, least privilege for SPNs, risky account protection     |
| Cloud Accounts                | MFA, device compliance, Identity Protection, CAE enforcement                        |

***

## 🎯 Final Summary

Defending against Initial Access in Entra ID focuses on:

* **Hardening user authentication paths (MFA, phishing-resistant auth)**
* **Monitoring consent and OAuth app behaviors**
* **Securing external identities and collaboration points**
* **Detecting and responding to risky sign-ins and credential misuse early**
