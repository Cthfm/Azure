# Defensive Strategies: TA0002

## **Defensive Strategies Against Execution in Entra ID (Azure Identity Environments)**

Execution in Entra ID typically happens through API calls (Graph API, Azure Resource Manager API) rather than traditional shell commands. Defense focuses on restricting API access, monitoring sensitive API operations, and controlling privileged identities.

***

### 💻 Command and Scripting Interpreter → Cloud API (T1059.009)

| Defensive Action                                                                                                                                                                                     | Why It Matters                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| 🔒 Apply Least Privilege (Principle of Least Privilege - PoLP) to all users, service principals, and managed identities                                                                              | Limit who can call powerful APIs                                          |
| 🚫 Use Privileged Identity Management (PIM) to make all privileged roles eligible and time-bound (no standing admin access)                                                                          | Prevent permanent exposure to Graph/ARM APIs                              |
| 📜 Enable Microsoft Entra ID (Azure AD) Audit Logs and sign-ins, then monitor for sensitive operations (user creation, group owner assignment, role elevation)                                       | Detect API abuse quickly                                                  |
| 🛡️ Require Administrative Unit (AU) scoping for admin accounts where possible                                                                                                                       | Limit what identities can manage via APIs                                 |
| 📜 Enable alerts in Microsoft Defender for Identity and Sentinel for abnormal API behaviors (e.g., sudden burst of user creations)                                                                   | Catch automation-based execution abuse                                    |
| 🚫 Restrict application permissions (delegated and app-only) in Entra ID App Registrations                                                                                                           | Prevent consented apps from misusing high-privilege Graph API permissions |
| 🔒 Enable and enforce Consent Governance: Only allow user consent to known/verified apps and require admin consent for high-risk permissions (e.g., `Directory.ReadWrite.All`, `User.ReadWrite.All`) | Stop rogue apps from silently executing admin API actions                 |
| 📜 Use Conditional Access policies to require compliant devices and/or MFA for all Graph API access to privileged resources                                                                          | Ensure trusted context even for API executions                            |

✅ **Effect**: API-based execution becomes much harder without being detected or blocked.

***

## 📊 **Defensive Coverage Table (Execution in Entra ID)**

| Attack Vector                | Defensive Strategy                                                                                                      |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Cloud API Abuse (Graph, ARM) | Least privilege, PIM, Audit Logs, AU scoping, app permission hardening, Defender monitoring, Conditional Access on APIs |

***

## 🎯 Final Summary

Defending against Execution in Entra ID focuses on:

* **Restricting who can run sensitive API operations** (limit create/modify actions)
* **Auditing and alerting on Graph API and ARM API calls**
* **Protecting privileged roles with PIM, CA policies, and device trust enforcement**
* **Blocking excessive application permissions and user consent risks**
