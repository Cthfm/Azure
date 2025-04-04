# Defensive Strategies: TA0004

## **Defensive Strategies Against Privilege Escalation in Entra ID**

Privilege escalation in Entra ID is **subtle but deadly** — attackers try to upgrade themselves silently through **roles, credentials, devices, or trust relationships**.

Defensive focus:\
➡️ **Strict control over role assignments and credentials**\
➡️ **Monitoring device registrations and trust changes**\
➡️ **Hardening PIM, Conditional Access, and federation settings**

***

### 🚀 Temporary Elevated Cloud Access (T1548.001)

| Defensive Action                                                                                               | Why It Matters                                   |
| -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| 🔒 Enable Privileged Identity Management (PIM) for all admin roles (Global Admin, Privileged Role Admin, etc.) | Time-bound, approval-required role elevation     |
| 🚫 Require MFA and justification for PIM activations                                                           | Make privilege escalation visible and deliberate |
| 📜 Alert on all role activation events (via Sentinel or Defender for Identity)                                 | Detect privilege activations immediately         |
| 🛡️ Use Just-In-Time (JIT) access review policies for critical roles                                           | Periodically validate PIM usage                  |

✅ **Effect**: Temporary privilege elevation is tightly monitored and controlled.

***

### 👥 Additional Cloud Credentials (T1098.001)

| Defensive Action                                                                          | Why It Matters                                  |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------- |
| 🔒 Rotate Service Principal credentials regularly                                         | Expire stale secrets/certs that could be abused |
| 🚫 Restrict who can modify Service Principal credentials (assign minimal app permissions) | Minimize credential addition abuse              |
| 📜 Monitor credential additions to Service Principals (Audit Logs)                        | Alert on suspicious new secrets or certificates |
| 🛡️ Prefer Managed Identities over app registrations                                      | No credentials = nothing to escalate            |

✅ **Effect**: Adding extra credentials stealthily becomes very difficult.

***

### 👥 Additional Cloud Roles (T1098.003)

| Defensive Action                                                                                   | Why It Matters                       |
| -------------------------------------------------------------------------------------------------- | ------------------------------------ |
| 🔒 Require PIM for all role assignments, even low-privilege ones                                   | No permanent hidden escalations      |
| 🚫 Review all role assignment changes weekly (Audit Logs + Access Reviews)                         | Catch unauthorized role grants early |
| 📜 Alert on assignment of sensitive roles (Global Admin, Privileged Auth Admin, Application Admin) | Immediate escalation detection       |

✅ **Effect**: Role escalation triggers alarms.

***

### 🖥️ Device Registration (T1098.004)

| Defensive Action                                                                                       | Why It Matters                                |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------- |
| 🔒 Restrict who can register devices (Device Settings → Users may join devices = selected groups only) | Prevent rogue device enrollments              |
| 🚫 Require device compliance and hybrid join for high-privilege access (Conditional Access)            | Force MDM-managed devices for sensitive roles |
| 📜 Monitor new device registrations, especially outside normal hours/IPs                               | Catch rogue devices                           |

✅ **Effect**: Attackers can’t "trust" fake devices easily.

***

### 🏢 Trust Modification (T1484.002)

| Defensive Action                                                                             | Why It Matters                               |
| -------------------------------------------------------------------------------------------- | -------------------------------------------- |
| 🔒 Lock down who can modify Azure B2B collaboration settings and external identity providers | Only Global Admins (via PIM)                 |
| 🚫 Disable auto-accept of federation and guest invites                                       | Manual approval only for new trusted domains |
| 📜 Monitor external identity provider changes and new B2B configurations                     | Catch trust tampering attempts               |

✅ **Effect**: Attackers can’t sneak in rogue trusted tenants or IDPs.

***

### 👤 Default Accounts (T1078.004)

| Defensive Action                                                                    | Why It Matters                             |
| ----------------------------------------------------------------------------------- | ------------------------------------------ |
| 🔒 Regularly audit default Service Principals, guest users, and automation accounts | Remove or restrict overprivileged defaults |
| 🚫 Enforce least privilege across all identities                                    | Shrink privilege footprint                 |
| 📜 Detect default accounts with excessive permissions (e.g., Contributor, Owner)    | Catch privilege creep early                |

✅ **Effect**: Defaults can’t silently escalate privileges.

***

### 👤 Cloud Accounts (T1078.004)

| Defensive Action                                                                                           | Why It Matters                         |
| ---------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| 🔒 Enforce MFA + Compliant Device + Risk-Based Conditional Access Policies for all cloud users             | Block use of stolen credentials alone  |
| 🚫 Use CA policies to auto-block risky users or suspicious logins (e.g., impossible travel, anonymous IPs) | Contain account hijacking fast         |
| 📜 Monitor privileged user sign-ins closely (especially logins from new devices or IPs)                    | Early detection of stolen admin access |

✅ **Effect**: Even if credentials are stolen, attackers can't easily escalate.

***

## 📊 **Defensive Coverage Table (Privilege Escalation in Entra ID)**

| Attack Vector                   | Defensive Strategy                                        |
| ------------------------------- | --------------------------------------------------------- |
| Temporary Elevated Cloud Access | PIM enforcement, role activation alerting                 |
| Additional Cloud Credentials    | Restrict SPN credential creation, audit secrets           |
| Additional Cloud Roles          | Lock down role assignments, review sensitive role changes |
| Device Registration             | Restrict who can register devices, require compliance     |
| Trust Modification              | Lock B2B and IdP modifications, monitor trust changes     |
| Default Accounts                | Audit and least-privilege default accounts                |
| Cloud Accounts                  | MFA, CA enforcement, risky login detection                |

***

## 🎯 Final Summary

Defending against Privilege Escalation in Entra ID focuses on:

* **Tightly controlling and monitoring elevated role usage**
* **Restricting credential additions and device registrations**
* **Hardening and reviewing trust configurations regularly**
* **Protecting against stolen credential reuse with strong access controls**

###
