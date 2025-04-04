# Defensive Strategies for TA0005

## **Defensive Strategies Against Defense Evasion in Entra ID**

Defense evasion in Entra ID is about **silencing logging**, **hiding identity changes**, **abusing token-based authentication**, and **weakening security enforcement**.

Your defense:\
➡️ **Lock critical paths** (logging, Conditional Access, MFA)\
➡️ **Detect trust manipulation and API token abuse early**\
➡️ **Control who can change security configurations**

***

### 🚀 Temporary Elevated Cloud Access (T1548.001)

| Defensive Action                                                                                    | Why It Matters                         |
| --------------------------------------------------------------------------------------------------- | -------------------------------------- |
| 🔒 Require Privileged Identity Management (PIM) for all privileged role activations                 | Time-bound, approved access            |
| 🚫 Enforce MFA + Approval + Justification for PIM activations                                       | Harder to hide privilege usage         |
| 📜 Monitor and alert on all PIM activations, especially Global Admin or Privileged Auth Admin roles | Detect suspicious privilege boosts     |
| 🛡️ Enable Access Reviews for all eligible PIM roles                                                | Periodically validate role assignments |

✅ **Effect**: Temporary privilege use is tightly watched.

***

### 🏢 Trust Modification (T1484.002)

| Defensive Action                                                                                              | Why It Matters                          |
| ------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| 🔒 Restrict modifications to external identity and B2B settings to a few trusted Global Admins (PIM enforced) | Limit who can alter trust relationships |
| 🚫 Require explicit approval for new federations or external domain trusts                                    | No automatic B2B acceptance             |
| 📜 Monitor changes to external identities and federation settings in Audit Logs                               | Catch unauthorized trust changes        |

✅ **Effect**: Federation and B2B abuse becomes visible.

***

### 💥 Disable or Modify Cloud Logs (T1562.008)

| Defensive Action                                                                     | Why It Matters                      |
| ------------------------------------------------------------------------------------ | ----------------------------------- |
| 🔒 Enforce Diagnostic Settings at the subscription level via Azure Policy            | Ensure logging can’t be disabled    |
| 🚫 Apply Resource Locks to logging resources (e.g., Log Analytics, Storage Accounts) | Prevent tampering with logs         |
| 📜 Alert on changes to Diagnostic Settings or Log Analytics configurations           | Detect log deletion or modification |
| 🛡️ Enable Immutable Logging (Microsoft Purview, Azure Monitor)                      | Create a tamper-proof audit trail   |

✅ **Effect**: Logs stay intact even if attackers try to disable them.

***

### 🔄 Modify Authentication Process

***

#### ➡️ Multi-Factor Authentication (T1556.006)

| Defensive Action                                                                                | Why It Matters                        |
| ----------------------------------------------------------------------------------------------- | ------------------------------------- |
| 🔒 Enforce strong MFA registration and recovery policies (Trusted MFA methods only)             | Protect MFA enrollment from attackers |
| 🚫 Require reauthentication for MFA device changes                                              | Make MFA modification noisy           |
| 📜 Monitor and alert on new MFA device registrations or resets                                  | Detect MFA evasion fast               |
| 🛡️ Enable Authentication Strength policies (Require FIDO2 or certificate-based MFA for admins) | Harden second-factor authentication   |

✅ **Effect**: MFA stays strong and hard to bypass.

***

#### ➡️ Hybrid Identity (T1556.007)

| Defensive Action                                                       | Why It Matters                   |
| ---------------------------------------------------------------------- | -------------------------------- |
| 🔒 Restrict Azure AD Connect configuration changes to select admins    | Secure the hybrid trust boundary |
| 🚫 Monitor and alert on unexpected Azure AD Connect sync modifications | Catch hybrid tampering           |
| 📜 Regularly audit synced users, groups, and permissions               | Detect rogue object syncing      |

✅ **Effect**: Hybrid identity can't be silently manipulated.

***

#### ➡️ Conditional Access Policies (T1556.008)

| Defensive Action                                                                     | Why It Matters                |
| ------------------------------------------------------------------------------------ | ----------------------------- |
| 🔒 Limit who can modify Conditional Access policies (Global Admin/PIM-enforced only) | Block unauthorized CA changes |
| 🚫 Require approval workflow for CA policy creation or editing                       | Add friction to changes       |
| 📜 Alert on any Conditional Access policy creation, modification, or deletion        | Detect policy weakening fast  |

✅ **Effect**: Attackers can’t silently lower defenses.

***

### 🔑 Application Access Token (T1550.001)

| Defensive Action                                                                                 | Why It Matters                         |
| ------------------------------------------------------------------------------------------------ | -------------------------------------- |
| 🔒 Implement short token lifetimes for OAuth refresh tokens                                      | Limit stolen token usability           |
| 🚫 Use Conditional Access policies requiring compliant devices and MFA even when tokens are used | Block stolen tokens                    |
| 📜 Monitor anomalous token reuse (same token, different IP/device)                               | Detect stolen token abuse              |
| 🛡️ Enable Continuous Access Evaluation (CAE)                                                    | Kill stolen sessions in near real-time |

✅ **Effect**: Even if tokens are stolen, access becomes hard.

***

### 👤 Default Accounts and Cloud Accounts (T1078.004)

| Defensive Action                                                                                        | Why It Matters               |
| ------------------------------------------------------------------------------------------------------- | ---------------------------- |
| 🔒 Regularly review and clean up default accounts (guest users, service principals, managed identities) | Remove attack surfaces       |
| 🚫 Apply Conditional Access to enforce MFA and compliant device checks for all accounts                 | Stop simple credential abuse |
| 📜 Detect impossible travel, risky IP logins, and legacy protocol usage                                 | Catch credential misuse fast |

✅ **Effect**: Accounts are hardened against stealth access.

***

## 📊 **Defensive Coverage Table (Defense Evasion in Entra ID)**

| Attack Vector                      | Defensive Strategy                                       |
| ---------------------------------- | -------------------------------------------------------- |
| Temporary Elevated Cloud Access    | PIM enforcement, audit activations                       |
| Trust Modification                 | Lock trust settings, audit external changes              |
| Disable or Modify Cloud Logs       | Enforce diagnostic settings, alert on changes            |
| Modify MFA                         | Secure MFA changes, monitor registrations                |
| Modify Hybrid Identity             | Lock hybrid config, audit synced objects                 |
| Modify Conditional Access Policies | Restrict and monitor CA changes                          |
| Application Access Token           | Short token lifetimes, Conditional Access on token usage |
| Default/Cloud Accounts             | Review defaults, enforce MFA and device compliance       |

***

## 🎯 Final Summary

Defending against Defense Evasion in Entra ID focuses on:

* **Securing privileged configurations (PIM, CA, B2B trust)**
* **Hardening token-based authentication paths**
* **Protecting logging infrastructure from tampering**
* **Monitoring all sensitive identity and authentication changes**
