# Defensive Strategies for TA0008

## **Defensive Strategies Against Lateral Movement in Entra ID**

Lateral movement in the cloud often **skips the network entirely** — it's **token-based and API-driven**.\
Defending against lateral movement means **protecting tokens**, **restricting their power**, and **detecting their misuse**.

***

### 🔑 Application Access Token (T1550.001)

| Defensive Action                                                                                                      | Why It Matters                                        |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| 🔒 Enforce strict Managed Identity permissions (Assign only required scopes via Azure RBAC)                           | Least privilege on tokens                             |
| 🚫 Shorten OAuth access and refresh token lifetimes                                                                   | Reduce window for token misuse                        |
| 🔒 Require Conditional Access for API access (device compliance, MFA) even when using tokens                          | Force strong context for token usage                  |
| 📜 Monitor Managed Identity usage and token access patterns (e.g., new IPs, new geographies)                          | Catch token reuse or unusual token behaviors          |
| 🚫 Enable **Continuous Access Evaluation (CAE)** for Entra ID tokens                                                  | Revoke compromised tokens in near real-time           |
| 🛡️ Secure the Azure Instance Metadata Service (IMDS) in VMs and Functions (Enable IMDSv2 or restrict network access) | Prevent easy local token theft                        |
| 🔒 Use User Assigned Managed Identities instead of System Assigned                                                    | Tighter scoping and auditing possible                 |
| 📜 Enable Defender for Cloud Apps OAuth app governance                                                                | Detect risky or compromised applications using tokens |
| 🔒 Limit or block "All App Permissions" OAuth grants unless absolutely necessary                                      | Prevent overprivileged app tokens                     |

✅ **Effect**: Token theft and reuse becomes risky and highly detectable for the attacker.

***

## 📊 **Defensive Coverage Table (Lateral Movement in Entra ID)**

| Attack Vector                  | Defensive Strategy                                                                                                                       |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Application Access Token Theft | Least privilege Managed Identity access, CA policies on tokens, token lifetime reduction, CAE enforcement, secure IMDS, OAuth governance |

***

## 🎯 Final Summary

Defending against Lateral Movement in Entra ID focuses on:

* **Protecting tokens like critical secrets**
* **Restricting what stolen tokens can access (least privilege everywhere)**
* **Monitoring how, where, and when tokens are used**
* **Revoking tokens quickly with Continuous Access Evaluation**
