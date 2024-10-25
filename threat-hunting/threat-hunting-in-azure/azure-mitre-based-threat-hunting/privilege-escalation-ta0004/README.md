---
hidden: true
---

# Privilege Escalation: TA0004

### **Overview**

**Privilege Escalation** refers to how attackers **gain higher-level permissions** within a compromised system to execute critical tasks, access sensitive data, or disable security controls. In **Azure environments**, privilege escalation often involves abusing misconfigurations, identities, and role assignments.

### **1. Abuse of Elevated Roles or Permissions**

**Technique: T1078 - Valid Accounts**\
Attackers leverage compromised credentials to gain access to higher privileges.

*   **T1078.004 - Cloud Accounts:**\
    _Azure Example:_ Use **stolen service principal tokens** to assign higher roles (like **Global Administrator**) to themselves:

    ```powershell
    Add-AzRoleAssignment -RoleDefinitionName "Global Administrator" -PrincipalId <AttackerID>
    ```

### **2. Exploiting Misconfigured Role Assignments**

**Technique: T1134 - Access Token Manipulation**\
Attackers manipulate access tokens to escalate privileges.

* **T1134.001 - Token Impersonation/Theft:**\
  _Azure Example:_ Use **OAuth tokens** from an exposed session to impersonate a privileged user and escalate privileges within Azure AD.

### **3. Exploiting Automation Accounts or Runbooks**

**Technique: T1548 - Abuse Elevation Control Mechanism**\
Attackers exploit privileged automation tools to run high-level tasks.

* **T1548.003 - Sudo and Sudo Caching Abuse:**\
  _Azure Example:_ Modify **Azure Automation Runbooks** to execute commands with elevated privileges.

### **4. Assigning or Modifying Role-Based Access Control (RBAC)**

**Technique: T1098 - Account Manipulation**\
Attackers manipulate roles or create privileged accounts.

*   **T1098.001 - Additional Cloud Credentials:**\
    _Azure Example:_ Use Azure CLI to assign the "Contributor" role to their service principal:

    ```bash
    az role assignment create --assignee <ServicePrincipalID> --role "Contributor"
    ```

### **5. Abuse of Vulnerable VM Configurations**

**Technique: T1068 - Exploitation for Privilege Escalation**\
Attackers exploit software vulnerabilities to escalate privileges.

* **Azure Example:** Use an **outdated kernel version** on an Azure Linux VM to escalate privileges with a kernel exploit like Dirty Cow.

### **6. Exploiting Misconfigured Conditional Access Policies**

**Technique: T1078.002 - Domain Accounts**\
Attackers exploit Azure AD misconfigurations to bypass security controls.

* **Azure Example:** Abuse a **misconfigured conditional access policy** to bypass MFA requirements for admin accounts.

### **7. Lateral Privilege Escalation Across Azure Tenants**

**Technique: T1199 - Trusted Relationship**\
Attackers leverage tenant-to-tenant trust to escalate privileges.

* **Azure Example:** Use an **application consent phishing attack** to gain access to a tenant where the app has privileged roles.

### **8. Abusing Service Principals for Privilege Escalation**

**Technique: T1098.003 - SSH Authorized Keys**\
Attackers modify authorized keys to gain root-level access to VMs.

* **Azure Example:** Upload SSH keys to a Linux VM to escalate privileges by gaining root access.

### **9. Elevating Privileges through API Abuse**

**Technique: T1106 - Native API**\
Attackers abuse APIs to assign themselves higher roles.

*   **Azure Example:** Use **Azure REST API** to escalate privileges by assigning "Global Administrator" to their account:

    ```bash
    curl -X POST -H "Authorization: Bearer <token>" "https://management.azure.com/subscriptions/{subID}/providers/Microsoft.Authorization/roleAssignments?api-version=2021-04-01"
    ```

***

### **Summary of Key Concepts with Techniques for TA0004**

| **Key Concept**                      | **Technique**                                 | **Azure Example**                                             |
| ------------------------------------ | --------------------------------------------- | ------------------------------------------------------------- |
| Abuse of Elevated Roles              | T1078 - Valid Accounts                        | Use stolen tokens to assign higher roles                      |
| Misconfigured Role Assignments       | T1134 - Access Token Manipulation             | Impersonate privileged users via OAuth token theft            |
| Exploiting Automation Accounts       | T1548 - Abuse Elevation Control Mechanism     | Modify runbooks for elevated execution                        |
| Assigning New Roles via RBAC         | T1098 - Account Manipulation                  | Assign "Contributor" role to service principal                |
| Exploiting Vulnerable Configurations | T1068 - Exploitation for Privilege Escalation | Kernel exploit on a Linux VM for root access                  |
| Misconfigured Conditional Access     | T1078.002 - Domain Accounts                   | Bypass MFA with conditional access loophole                   |
| Lateral Privilege Escalation         | T1199 - Trusted Relationship                  | Use consent phishing to access privileged apps across tenants |
| Abusing Service Principals           | T1098.003 - SSH Authorized Keys               | Upload SSH key for root access on Linux VM                    |
| Privilege Escalation via APIs        | T1106 - Native API                            | Assign Global Admin role using Azure REST API                 |
