---
hidden: true
---

# Discovery: TA0007

## Overview

The Discovery tactic focuses on how attackers gather information about the target environment after gaining access. In Azure environments, discovery enables attackers to understand network topologies, permissions, services, and accounts, helping them plan lateral movement, privilege escalation, or exfiltration. Below is a breakdown of key concepts, techniques, and Azure-specific procedures for TA0007.

### **1. Identifying Active Directory and Azure AD Objects**

**Technique:** T1087 - Account Discovery\
Attackers enumerate **user accounts, groups, or service principals** in Azure AD to identify high-value targets.

*   **T1087.002 - Domain Account**\
    **Azure Example:** Use **Azure CLI** to list users and groups from Azure AD.

    ```bash
    az ad user list --query '[].{Name:displayName,User:userPrincipalName}' --output table
    az ad group list --output table
    ```

***

### **2. Enumerating Roles and Permissions**

**Technique:** T1069 - Permission Groups Discovery\
Attackers gather information about **RBAC (Role-Based Access Control) roles** and **group memberships** to understand permissions and privilege escalation paths.

*   **T1069.002 - Domain Groups**\
    **Azure Example:** Enumerate **Azure AD role assignments** to identify accounts with elevated privileges.

    ```bash
    az role assignment list --query '[].{Role:roleDefinitionName,Principal:principalName}' --output table
    ```

***

### **3. Discovering Network Configuration and Security Rules**

**Technique:** T1016 - System Network Configuration Discovery\
Attackers map out the **network topology and firewall rules** to identify open ports or misconfigurations.

*   Use **Azure CLI** to list virtual networks (VNets) and security group rules.

    ```bash
    az network vnet list --output table
    az network nsg rule list --nsg-name <NSG_NAME> --resource-group <RESOURCE_GROUP> --output table
    ```

### **4. Querying Cloud Services and Resources**

**Technique:** T1057 - Process Discovery\
Attackers gather information about **active cloud services** such as VMs, storage accounts, or databases to identify targets for further exploitation.

*   List running VMs, storage accounts, and databases using **Azure CLI**.

    ```bash
    az vm list --output table
    az storage account list --output table
    az sql server list --output table
    ```

### **5. Enumerating Automation Accounts and Runbooks**

**Technique:** T1083 - File and Directory Discovery\
Attackers search for **automation tasks and runbooks** that might contain hardcoded credentials or critical scripts.

*   Use Azure CLI to list automation accounts and their runbooks.

    ```bash
    az automation account list --output table
    az automation runbook list --automation-account-name <AUTOMATION_ACCOUNT> --resource-group <RESOURCE_GROUP>
    ```

### **6. Identifying Cloud Metadata and IAM Roles**

**Technique:** T1552.004 - Credentials in Cloud Metadata\
Attackers query **instance metadata services** on Azure VMs to identify IAM roles and obtain temporary access tokens.

*   Query **IMDS** on a compromised VM to retrieve metadata and tokens.

    ```bash
    curl -H "Metadata: true" http://169.254.169.254/metadata/instance?api-version=2021-02-01
    ```

***

### **7. Discovering Security Tools and Defenses**

**Technique:** T1518 - Software Discovery\
Attackers gather information about installed security tools to evade detection and avoid triggering alerts.

*   Use **Azure CLI** to identify **Defender for Cloud configurations** or **monitoring agents**.

    ```bash
    az security pricing list --output table
    az vm extension list --query "[?type=='Microsoft.Azure.Monitoring.Agent']" --output table
    ```

***

### **8. Mapping Virtual Networks and Peering Connections**

**Technique:** T1018 - Remote System Discovery\
Attackers map **VNet peering connections** to understand network segmentation and lateral movement opportunities.

*   List **VNet peering** connections to identify accessible subnets.

    ```bash
    az network vnet peering list --vnet-name <VNET_NAME> --resource-group <RESOURCE_GROUP> --output table
    ```

### **9. Listing Privileged Users and Service Principals**

**Technique:** T1069.001 - Local Groups Discovery\
Attackers search for **privileged Azure AD roles** to identify accounts or service principals with admin permissions.

*   Enumerate all users with the **Global Administrator role**.

    ```bash
    az ad user list --filter "assignedRoles/any(r:r/roleDefinitionName eq 'Global Administrator')" --output table
    ```

***

### **Summary of Key Concepts with Techniques for TA0007**

| **Key Concept**                        | **Technique**                                  | **Azure Example**                                     |
| -------------------------------------- | ---------------------------------------------- | ----------------------------------------------------- |
| Identifying AD Users and Groups        | T1087 - Account Discovery                      | List users and groups in Azure AD                     |
| Enumerating RBAC Roles and Permissions | T1069 - Permission Groups Discovery            | List role assignments and permissions                 |
| Discovering Network Configurations     | T1016 - System Network Configuration Discovery | List VNets and NSG rules                              |
| Querying Active Services and Resources | T1057 - Process Discovery                      | List VMs, storage accounts, and databases             |
| Enumerating Automation Tasks           | T1083 - File and Directory Discovery           | List automation accounts and runbooks                 |
| Identifying Cloud Metadata and Tokens  | T1552.004 - Credentials in Cloud Metadata      | Query IMDS for IAM roles and tokens                   |
| Discovering Security Tools             | T1518 - Software Discovery                     | Identify monitoring tools and Defender configurations |
| Mapping VNet Peering Connections       | T1018 - Remote System Discovery                | List VNet peering connections                         |
| Listing Privileged Accounts            | T1069.001 - Local Groups Discovery             | Identify Global Administrators and service principals |
