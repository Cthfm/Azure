# Defensive Strategies: TA0007

## Defensive Strategies for TA0007 - Discovery

The Discovery (TA0007) tactic involves attackers gathering critical information about accounts, resources, and configurations to plan subsequent moves. Defending against these activities in Entra ID environments requires monitoring, restricting permissions, and hardening configurations to limit exposure.

### **1. Account Discovery**

**Mitigates:** T1087 - Account Discovery\
**Action:** Prevent attackers from enumerating Entra ID accounts to identify potential targets.\
**Azure Procedure:**

* Use **Role-Based Access Control (RBAC)** to restrict directory enumeration to least privilege.
* Enable **audit logging** and set alerts for user enumeration attempts in **Entra ID audit logs**.
* Apply **Conditional Access Policies** to enforce MFA and restrict access to sensitive APIs.

### **2. Cloud Account Enumeration**

**Mitigates:** T1087.004 - Cloud Account\
**Action:** Prevent attackers from locating valuable or privileged accounts in Entra ID.\
**Azure Procedure:**

* Monitor for suspicious commands such as `Get-AzADUser`.
* Restrict **API** and **CLI permissions** to authorized users only.
* Enable **Azure Security Defaults** to enforce MFA for all users automatically.

### **3. Cloud Service Dashboard Access**

**Mitigates:** T1087 - Cloud Service Dashboard\
**Action:** Block unauthorized access to the Azure Portal and prevent attackers from exploring services and configurations.\
**Azure Procedure:**

* Enforce **RBAC** to limit portal access to essential personnel.
* Require the use of **privileged access workstations (PAWs)** for administrative tasks.
* Conduct **regular access reviews** to identify and remove unnecessary access.

### **4. Cloud Service Discovery**

**Mitigates:** T1526 - Cloud Service Discovery\
**Action:** Prevent attackers from using CLI, APIs, or dashboards to list cloud services and resources.\
**Azure Procedure:**

* Disable unused Azure services to reduce the attack surface.
*   Monitor and set alerts for commands like:

    ```bash
    az resource list --output table
    ```
* Implement service principal restrictions and enforce **least privilege** for API calls.

### **5. Password Policy Discovery**

**Mitigates:** T1201 - Password Policy Discovery\
**Action:** Prevent attackers from querying Entra ID password policies to inform brute-force or credential stuffing attacks.\
**Azure Procedure:**

* Enable strong password policies using **banned password lists**.
* Monitor changes to password policies via **Entra audit logs** and set alerts.
* Use **Smart Lockout** to block brute-force attempts based on behavior analysis.

### **6. Permission Groups Discovery**

**Mitigates:** T1069 - Permission Groups Discovery\
**Action:** Block unauthorized enumeration of groups to identify privileged or misconfigured group memberships.\
**Azure Procedure:**

* Restrict group enumeration permissions to necessary roles only.
* Implement **Privileged Identity Management (PIM)** for critical groups, such as Global Administrators.
* Monitor group changes using **Azure Monitor** or **Microsoft Sentinel**.

### **7. Cloud Groups Enumeration**

**Mitigates:** T1069.003 - Cloud Groups\
**Action:** Prevent attackers from enumerating Entra ID cloud groups to locate administrative or sensitive access roles.\
**Azure Procedure:**

*   Monitor and restrict the use of commands such as:

    ```bash
    az ad group list --output table
    az ad group member list --output table
    ```
* Conduct regular access reviews of sensitive groups to detect unauthorized access.
* Enforce **just-in-time (JIT)** access for administrative groups using **PIM**.

### **Summary of Defensive Procedures for TA0007**

<table data-header-hidden><thead><tr><th width="292"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Defensive Strategy</strong></td><td><strong>Mitigates</strong></td><td><strong>Azure Procedure</strong></td></tr><tr><td>Monitor and Restrict Account Discovery</td><td>T1087 - Account Discovery</td><td>- Use RBAC to restrict directory enumeration to least privilege.<br>- Enable audit logging and alerts for user enumeration.<br>- Apply Conditional Access Policies to enforce MFA and restrict access to sensitive APIs.</td></tr><tr><td>Monitor Cloud Account Enumeration</td><td>T1087.004 - Cloud Account</td><td>- Monitor for suspicious commands like <code>Get-AzADUser</code>.<br>- Restrict API and CLI permissions to authorized users.<br>- Enable Azure Security Defaults to enforce MFA for all users automatically.</td></tr><tr><td>Restrict Cloud Service Dashboard Access</td><td>T1087 - Cloud Service Dashboard</td><td>- Enforce RBAC to limit portal access.<br>- Require the use of privileged access workstations (PAWs) for administrative tasks.<br>- Conduct regular access reviews to remove unnecessary access.</td></tr><tr><td>Prevent Unauthorized Cloud Service Discovery</td><td>T1526 - Cloud Service Discovery</td><td>- Disable unused Azure services.<br>- Monitor and set alerts for commands like <code>az resource list --output table</code>.<br>- Implement service principal restrictions and enforce least privilege.</td></tr><tr><td>Monitor Password Policy Discovery Attempts</td><td>T1201 - Password Policy Discovery</td><td>- Enable strong password policies using banned password lists.<br>- Monitor changes to password policies via Entra audit logs and set alerts.<br>- Use Smart Lockout to block brute-force attempts.</td></tr><tr><td>Block Permission Groups Enumeration</td><td>T1069 - Permission Groups Discovery</td><td>- Restrict group enumeration permissions to necessary roles.<br>- Implement PIM for critical groups like Global Administrators.<br>- Monitor group changes using Azure Monitor or Microsoft Sentinel.</td></tr><tr><td>Detect Cloud Groups Enumeration Attempts</td><td>T1069.003 - Cloud Groups</td><td>- Monitor and restrict commands like <code>az ad group list</code> and <code>az ad group member list</code>.<br>- Conduct access reviews of sensitive groups.<br>- Enforce JIT access for administrative groups using PIM.</td></tr></tbody></table>

