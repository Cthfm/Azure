# Defensive Strategies: TA0007

## **Defensive Strategies Against Discovery in Entra ID (Azure Identity Environments)**

Discovery is **pre-attack mapping** — adversaries try to learn your cloud identities, services, and permissions.\
Defense focuses on **restricting enumeration**, **detecting reconnaissance**, and **minimizing unnecessary exposure**.

***

### 🔍 Cloud Account Discovery (T1087.004)

| Defensive Action                                                                                              | Why It Matters                                    |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| 🔒 Apply least privilege across users and service principals                                                  | Limit who can list or enumerate directory objects |
| 🚫 Use Administrative Units (AU) in Entra ID to scope visibility                                              | Isolate sensitive users and groups                |
| 📜 Enable Azure AD Sign-In and Audit Logging                                                                  | Detect suspicious enumeration queries             |
| 🛡️ Monitor mass read operations on Entra ID users and service principals (e.g., high volume Graph API reads) | Catch reconnaissance patterns early               |

✅ **Effect**: Mass user/service principal enumeration becomes visible and noisy.

***

### 🖥️ Cloud Service Dashboard & Cloud Service Discovery (T1087.004 extension)

| Defensive Action                                                                                      | Why It Matters                           |
| ----------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| 🔒 Use Role-Based Access Control (RBAC) to restrict access to Azure resources and Azure Portal views  | Prevent unauthorized resource visibility |
| 🚫 Apply **Reader** or **Monitoring Reader** roles only where needed                                  | No broad read access                     |
| 📜 Monitor Azure Resource Graph queries and list operations (e.g., resource.list, VM.list)            | Spot discovery behavior                  |
| 🛡️ Use Azure Activity Logs and Microsoft Defender for Cloud to detect unauthorized resource browsing |                                          |

✅ **Effect**: Attackers can't "map" services silently.

***

### 🔑 Password Policy Discovery (T1201)

| Defensive Action                                                                                      | Why It Matters                                          |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| 🔒 Enforce strong Entra ID Password Protection policies (global banned passwords, custom banned list) | Even if policies are discovered, attacks stay difficult |
| 🚫 Prevent read access to sensitive tenant configurations unless required (Graph API access control)  | Hide password policy settings from regular users        |
| 📜 Monitor Graph API calls that access password policy settings                                       | Detect policy reconnaissance attempts                   |

✅ **Effect**: Even if discovered, password policies remain strong and resilient.

***

### 👥 Cloud Groups Discovery (T1069.003)

| Defensive Action                                                                                   | Why It Matters                                     |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| 🔒 Limit who can list groups or enumerate group memberships (Graph API permissions hardening)      | Prevent broad group visibility                     |
| 🚫 Use Administrative Units to segment group visibility by department, project, or function        | No tenant-wide group visibility                    |
| 📜 Monitor for enumeration of sensitive groups (e.g., Global Admins, Privileged Role Admins)       | Detect when an attacker maps control groups        |
| 🛡️ Enable risk-based Conditional Access requiring additional verification for admin group members | Protect privileged users/groups even if enumerated |

✅ **Effect**: Privilege structures stay hidden and protected.

***

## 📊 **Defensive Coverage Table (Discovery in Entra ID)**

| Attack Vector                     | Defensive Strategy                                                   |
| --------------------------------- | -------------------------------------------------------------------- |
| Cloud Account Discovery           | Least privilege, Administrative Units, detect mass user enumeration  |
| Cloud Service Dashboard/Discovery | RBAC enforcement, resource graph monitoring                          |
| Password Policy Discovery         | Strong policies, prevent policy reads, monitor API access            |
| Cloud Groups Discovery            | Limit group enumeration, segment groups via AUs, monitor group reads |

***

## 🎯 Final Summary

Defending against Discovery in Entra ID focuses on:

* **Restricting visibility to only what’s necessary**
* **Applying least privilege to identities and resources**
* **Detecting mass enumeration attempts early**
* **Segmenting and isolating sensitive information and identities**

