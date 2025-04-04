# Defensive Strategies: TA0003

## **Defensive Strategies Against Persistence in Entra ID (Azure Identity Environments)**

Persistence in Entra ID is subtle — often hiding in **accounts, roles, tokens, device registrations, or authentication flows**.\
Defense focuses on **tight identity governance, monitoring sensitive changes**, and **detecting unauthorized persistence attempts early**.

***

### 👥 Account Manipulation

***

#### ➡️ Additional Cloud Credentials (T1098.001)

| Defensive Action                                                                       | Why It Matters                         |
| -------------------------------------------------------------------------------------- | -------------------------------------- |
| 🔒 Enforce credential expiration policies for service principals (short-lived secrets) | Prevent persistent credential abuse    |
| 🚫 Rotate service principal secrets and certificates regularly                         | Invalidate stale/persisted credentials |
| 📜 Enable Defender for Cloud Apps and audit service principal secret additions         | Detect rogue credential creations      |
| 🛡️ Use Managed Identities where possible (no credentials to steal)                    | Reduce attack surface                  |

✅ **Effect**: Attackers can’t add long-lived credentials quietly.

***

#### ➡️ Additional Cloud Roles (T1098.003)

| Defensive Action                                                | Why It Matters                                 |
| --------------------------------------------------------------- | ---------------------------------------------- |
| 🔒 Use Privileged Identity Management (PIM) for all admin roles | Only time-bound, approved privilege escalation |
| 🚫 Require approval workflows and MFA for role activations      | Block unauthorized role assignments            |
| 📜 Monitor Azure AD Audit Logs for role assignment events       | Detect privilege escalations immediately       |

✅ **Effect**: Role persistence is caught and blocked fast.

***

#### ➡️ Device Registration (T1098.004)

| Defensive Action                                                    | Why It Matters                      |
| ------------------------------------------------------------------- | ----------------------------------- |
| 🔒 Limit who can register devices in Entra ID (device settings)     | Prevent rogue device registrations  |
| 🚫 Require device compliance checks for Conditional Access policies | Block non-compliant rogue devices   |
| 📜 Monitor new device registrations, especially from unusual IPs    | Catch suspicious device enrollments |

✅ **Effect**: Attackers can’t use fake trusted devices to persist access.

***

### ➕ Create Cloud Account (T1136.003)

| Defensive Action                                         | Why It Matters                        |
| -------------------------------------------------------- | ------------------------------------- |
| 🔒 Restrict user creation rights to Identity Admins only | No random user creations              |
| 🚫 Enforce MFA for all privileged operations             | Stop silent backdoor account creation |
| 📜 Alert on new user creation events in Entra ID logs    | Detect persistence fast               |

✅ **Effect**: Hidden user accounts are detected and blocked.

***

### 🔄 Modify Authentication Process

***

#### ➡️ Multi-Factor Authentication (T1556.006)

| Defensive Action                                                                 | Why It Matters                   |
| -------------------------------------------------------------------------------- | -------------------------------- |
| 🔒 Require MFA re-registration approval (MFA Registration Policy)                | Stop silent MFA method takeovers |
| 🚫 Lock MFA methods via Identity Protection policies (Trusted MFA Registrations) | Secure second factors tightly    |
| 📜 Monitor MFA registration and reset events (Azure AD logs)                     | Detect suspicious MFA changes    |

✅ **Effect**: Attackers can’t persist by hijacking MFA.

***

#### ➡️ Hybrid Identity (T1556.007)

| Defensive Action                                                 | Why It Matters                     |
| ---------------------------------------------------------------- | ---------------------------------- |
| 🔒 Harden Azure AD Connect sync configurations (limited OU sync) | Control what flows into Entra ID   |
| 🚫 Monitor synchronization changes and sync errors               | Detect unauthorized hybrid changes |
| 📜 Regularly audit synced objects for unexpected users or groups | Spot hidden persistence routes     |

✅ **Effect**: On-prem attacks can’t create cloud persistence easily.

***

#### ➡️ Conditional Access Policies (T1556.008)

| Defensive Action                                                              | Why It Matters                              |
| ----------------------------------------------------------------------------- | ------------------------------------------- |
| 🔒 Lock down Conditional Access policy management (Global Admins only + PIM)  | Prevent CA tampering                        |
| 🚫 Require approval for CA policy edits                                       | Force peer review of access changes         |
| 📜 Monitor CA policy changes (Audit Logs) and alert on disables or exclusions | Detect weakening of protections immediately |

✅ **Effect**: Attackers can’t modify policies to maintain stealthy access.

***

### 👤 Valid Accounts (Default Accounts and Cloud Accounts)

***

#### ➡️ Default Accounts (T1078.004)

| Defensive Action                                                            | Why It Matters                  |
| --------------------------------------------------------------------------- | ------------------------------- |
| 🔒 Regularly review guest users, service principals, and managed identities | Remove stale accounts           |
| 🚫 Apply least privilege to default and automation accounts                 | Minimize their impact if abused |
| 📜 Enable risky account detection in Identity Protection                    | Catch compromised defaults fast |

✅ **Effect**: Defaults are hardened and monitored constantly.

***

#### ➡️ Cloud Accounts (T1078.004)

| Defensive Action                                                             | Why It Matters                        |
| ---------------------------------------------------------------------------- | ------------------------------------- |
| 🔒 Enforce MFA and compliant device policies for all cloud users             | Block simple stolen credential use    |
| 🚫 Enable Conditional Access Risk Policies (block risky users automatically) | Cut off compromised users immediately |
| 📜 Monitor impossible travel, unfamiliar sign-in anomalies                   | Detect stolen session reuse fast      |

✅ **Effect**: Even stolen credentials don’t guarantee persistence.

***

## 📊 **Defensive Coverage Table (Persistence in Entra ID)**

| Attack Vector                | Defensive Strategy                                 |
| ---------------------------- | -------------------------------------------------- |
| Additional Cloud Credentials | Rotate secrets, audit SPN credential changes       |
| Additional Cloud Roles       | Use PIM, alert on role assignments                 |
| Device Registration          | Restrict device registration, monitor new devices  |
| Create Cloud Account         | Lock user creation, alert on new users             |
| Modify MFA                   | Secure MFA registration/reset, monitor MFA changes |
| Modify Hybrid Identity       | Harden Azure AD Connect, monitor hybrid changes    |
| Modify Conditional Access    | Lock CA editing rights, alert on policy changes    |
| Default Accounts             | Review and harden guest/SPN accounts               |
| Cloud Accounts               | Enforce MFA, detect risky sign-ins                 |

***

## 🎯 Final Summary

Defending against persistence in Entra ID focuses on:

* **Locking down identity lifecycle management (creation, credential changes, device enrollments)**
* **Hardening authentication flows (MFA, CA policies)**
* **Monitoring privileged operations (role assignments, policy edits)**
* **Detecting stale or risky accounts early**
