---
hidden: true
---

# Privilege Escalation: TA0004

### **Overview**

**Privilege Escalation** refers to how attackers **gain higher-level permissions** within a compromised system to execute critical tasks, access sensitive data, or disable security controls. In **Azure environments**, privilege escalation often involves abusing misconfigurations, identities, and role assignments.

### **1.** Abuse Elevation Control Mechanism

**Technique: T1548 - Abuse Elevation Control Mechanism**\
Attackers circumvent systems that are designed to elevate a principal's access and gain higher privileges.

* **T1548.005 - Temporary Elevated Cloud Access**\
  Attackers utilize the 'Automatic' Approval Mode within the JIT Configuration in order to obtain elevated privilege.&#x20;

### **2.** Account Manipulation

**Technique: T1098 - Account Manipulation**\
Attackers may manipulate accounts to maintain or elevate access to victim systems. This may involve actions like modifying credentials or permission groups to retain control. Attackers might also subvert security policies, such as repeatedly updating passwords to bypass duration policies and extend compromised access.

* **T1098.001 - Additional Cloud Credentials**\
  Generating SAS tokens in order to maintain access to an organization's storage account data. Attackers can also add credentials to OAuth Application "App Registrations" in order to elevate privileges.

{% code overflow="wrap" fullWidth="false" %}
```bash
$sasToken = New-AzStorageContainerSASToken -Name $containerName -Context $context         -Permission rwdl -ExpiryTime (Get-Date).AddDays(900)
```
{% endcode %}

* **T1098.003 - Additional Cloud Roles**\
  Attacker creates additional roles with a compromised user

```powershell
$userId = (Get-AzADUser -UserPrincipalName "compromised_user@example.com").Id $roleDefinition = Get-AzRoleDefinition -Name "Contributor"
$roleDefinition = Get-AzRoleDefinition -Name "Contributor"

New-AzRoleAssignment -ObjectId $userId -RoleDefinitionName $roleDefinition.Name -Scope "/subscriptions/<SubscriptionID>/ResourceGroups/CompanySecrets"
```

* **T1098.005 - Registered Device**\
  Attackers that already have initial access will modify existing Intune policies to register a rouge device.

### **3.** Domain or Tenant Policy Modification

**Technique: T1484 - Abuse Elevation Control Mechanism**\
Attackers exploit privileged automation tools to run high-level tasks.

* **T1484.002- Trust Modification**\
  Attackers can manipulate domain trust configurations to evade defenses or escalate privileges. By adding new domain trusts, modifying existing ones, or adjusting trust properties, they can redefine authentication and authorization flows between domains or tenants. These trust relationships, particularly for federated identities, govern access to shared resources and can include sensitive elements like accounts, credentials, and tokens applied across servers and domains.

### **4. Valid Accounts**

**Technique:** T1078 **- Valid Accounts**\
Attackers may obtain and abuse credentials of existing accounts as a means of gaining

* **T1078.001 - Default Accounts**\
  Attacker utilized default usernames and passwords in order to gain access to establish persistence.
* **T1556.003 - Cloud Accounts**\
  Attacker is able to compromise an account in order to get access. This can be done a myriad of ways that include phishing, brute forcing, and other mechanisms.&#x20;

### **Summary of Key Concepts with Techniques for TA0004**

| Key Concept                              | Technique                                     | Azure Example                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------- | --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ab**use Elevation Control Mechanism**    | **T1548 - Abuse Elevation Control Mechanism** | <p><strong>T1548.005 - Temporary Elevated Cloud Access</strong><br>Attackers use 'Automatic' Approval Mode in JIT to obtain elevated privilege.</p>                                                                                                                                                                                                                                                                                                                   |
| **Account Manipulation**                 | **T1098 - Account Manipulation**              | <p><strong>T1098.001 - Additional Cloud Credentials</strong><br>Generate SAS tokens to maintain storage account access.<br><code>$sasToken = New-AzStorageContainerSASToken -Name $containerName -Context $context -Permission rwdl -ExpiryTime (Get-Date).AddDays(900)</code></p>                                                                                                                                                                                    |
| A**ccount Manipulation**                 | **T1098 - Account Manipulation**              | <p><strong>T1098.003 - Additional Cloud Roles</strong><br>Add roles to compromised user for elevated access:<br><code>$userId = (Get-AzADUser -UserPrincipalName "compromised_user@example.com").Id</code><br><code>$roleDefinition = Get-AzRoleDefinition -Name "Contributor"</code><br><code>New-AzRoleAssignment -ObjectId $userId -RoleDefinitionName $roleDefinition.Name -Scope "/subscriptions/&#x3C;SubscriptionID>/ResourceGroups/CompanySecrets"</code></p> |
| A**ccount Manipulation**                 | **T1098 - Account Manipulation**              | <p><strong>T1098.005 - Registered Device</strong><br>Modify Intune policies to register rogue devices.</p>                                                                                                                                                                                                                                                                                                                                                            |
| **Domain or Tenant Policy Modification** | **Domain or Tenant Policy Modification**      | <p><strong>T1484.002 - Trust Modification</strong><br>Manipulate domain trust configurations to evade defenses or escalate privileges by adding or modifying trusts. Trusted relationships for federated identities control access to shared resources, including accounts and tokens.</p>                                                                                                                                                                            |
| **Valid Accounts**                       | **T1078 - Valid Accounts**                    | <p><strong>T1078.001 - Default Accounts</strong><br>Exploit default credentials for access and persistence.</p>                                                                                                                                                                                                                                                                                                                                                       |
| **Valid Accounts**                       | **T1078 - Valid Accounts**                    | <p><strong>T1556.003 - Cloud Accounts</strong><br>Attacker is able to compromise an account in order to get access. This can be done a myriad of ways that include phishing, brute forcing, and other mechanisms. </p>                                                                                                                                                                                                                                                |

