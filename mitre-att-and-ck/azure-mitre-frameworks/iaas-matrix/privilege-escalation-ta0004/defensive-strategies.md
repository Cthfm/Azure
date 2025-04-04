# Defensive Strategies

## **Defensive Strategies Against Privilege Escalation in Azure Environments**

In Azure, defending against Privilege Escalation requires **tight control over identities, role assignments, cloud automation**, and **real-time detection of privilege changes**.\
If you lock down escalation paths, you limit the blast radius dramatically.

***

### ⬆️ Abuse Elevation Control Mechanism → Temporary Elevated Cloud Access (T1548)

| Defensive Action                                                                                   | Why It Matters                                         |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| 🔒 Require approval workflows for PIM JIT activations (Azure PIM)                                  | Prevent attackers from silently elevating privileges   |
| 🚫 Restrict privileged role assignment only to designated admins (Privileged Role Admin role only) | Control who can manage roles like Owner, Contributor   |
| 📜 Monitor PIM activations via Azure AD Sign-In Logs and activate alerts                           | Detect unusual or unapproved JIT activations           |
| 🛡️ Use Conditional Access policies requiring compliant devices or MFA for PIM activations         | Make elevation harder even if attacker has credentials |

✅ **Effect**: Attackers can’t easily abuse PIM or JIT to escalate unnoticed.

***

### 👤 Account Manipulation → Additional Cloud Credentials (T1098.001)

| Defensive Action                                                                                                                | Why It Matters                                    |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| 🔒 Limit who can create or modify Service Principal credentials (Application Administrator, Cloud App Administrator roles only) | Stop hidden credential additions                  |
| 🚫 Use Azure Policy to block Service Principals without expiration on secrets                                                   | Force rotation and prevent stale keys             |
| 📜 Alert on Service Principal credential changes via Defender for Identity                                                      | Real-time visibility into credential manipulation |

✅ **Effect**: Attackers can't add their own secrets easily to maintain access.

***

### 👤 Account Manipulation → Additional Cloud Roles (T1098.003)

| Defensive Action                                                                                               | Why It Matters                              |
| -------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| 🔒 Use Role-Based Access Control (RBAC) to restrict who can assign roles at subscription/resource group levels | Prevent mass privilege escalation           |
| 🚫 Require privileged role assignments to go through PIM activation and approval                               | Control access creep dynamically            |
| 📜 Alert on new role assignments, especially Contributor/Owner roles, using Azure Monitor or Sentinel          | Detect privilege escalations as they happen |

✅ **Effect**: Catch role escalation early before it’s weaponized.

***

### 👤 Account Manipulation → SSH Authorized Keys (T1098.004)

| Defensive Action                                                                          | Why It Matters                                |
| ----------------------------------------------------------------------------------------- | --------------------------------------------- |
| 🔒 Disable CustomScript and VMAccess extensions after deployment unless explicitly needed | Block external SSH key injection vectors      |
| 🚫 Block privileged users from attaching SSH keys without strong audit                    | Limit ability to inject keys without tracking |
| 📜 Monitor VM extension deployments and SSH key changes through Azure Activity Logs       | Detect key tampering attempts fast            |

✅ **Effect**: Prevent attackers from inserting SSH keys to VMs silently.

***

### 📅 Event Triggered Execution (T1546)

| Defensive Action                                                                             | Why It Matters                          |
| -------------------------------------------------------------------------------------------- | --------------------------------------- |
| 🔒 Restrict who can create or modify Logic Apps, Functions, and Event Grid Subscriptions     | Reduce persistence and escalation risk  |
| 🚫 Apply Azure Policies to control serverless deployments to trusted resource groups only    | No rogue serverless deployments allowed |
| 📜 Alert on new serverless resource creations (Functions, Logic Apps) via Defender for Cloud | Detect malicious trigger setups         |

✅ **Effect**: Attackers can’t silently set auto-privilege escalation triggers.

***

### 👥 Valid Accounts → Default Accounts / Cloud Accounts (T1078.004)

| Defensive Action                                                                                     | Why It Matters                              |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| 🔒 Identify and disable unused Service Principals, managed identities, and default accounts          | Shrink attack surface                       |
| 🚫 Apply Conditional Access policies requiring MFA for all privileged users                          | Stop stolen credentials from working easily |
| 📜 Monitor login behavior for anomalies (impossible travel, new locations) using Identity Protection | Early credential abuse detection            |
| 🛡️ Use Smart Lockout policies to block brute force or credential stuffing                           | Strengthen default defenses on accounts     |

✅ **Effect**: Reduces cloud account abuse for privilege escalation.

***

## 📊 **Defensive Coverage Table (Privilege Escalation in Azure)**

| Attack Vector                   | Defensive Strategy                                                       |
| ------------------------------- | ------------------------------------------------------------------------ |
| Temporary Elevated Cloud Access | PIM approvals, JIT monitoring, CA enforcement                            |
| Additional Cloud Credentials    | SPN credential restrictions, expiration enforcement, Defender monitoring |
| Additional Cloud Roles          | Restrict role assignment rights, monitor new privileged roles            |
| SSH Authorized Keys             | Block/monitor VM extensions, disable unused access methods               |
| Event Triggered Execution       | Control serverless creation, monitor new Logic Apps/Functions            |
| Default/Cloud Accounts          | Disable defaults, require MFA, detect login anomalies                    |

***

## 🎯 Final Summary

Defending against Privilege Escalation in Azure focuses on:

* **Tightly controlling identity and role assignments** (PIM, RBAC lockdowns)
* **Preventing unauthorized credential modifications** (SPN secret control)
* **Monitoring and alerting on key privilege changes** (role assignments, function deployments)
* **Hardening access methods and detecting credential misuse fast**

