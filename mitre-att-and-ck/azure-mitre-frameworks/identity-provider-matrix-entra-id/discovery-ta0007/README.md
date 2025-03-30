# Discovery: TA0007

## Overview

The Discovery tactic focuses on how attackers gather information about the target environment after gaining access. In Azure environments, discovery enables attackers to understand network topologies, permissions, services, and accounts, helping them plan lateral movement, privilege escalation, or exfiltration. Below is a breakdown of key concepts, techniques, and Azure-specific procedures for TA0007.

### 1. **Account Discovery (T1087)**

* **Cloud Account Discovery (T1087.004):** Attackers enumerate Entra ID accounts to identify potential targets.
  *   **Example:** Using Entra PowerShell to list all users in the directory:

      ```powershell
      Get-AzADUser
      ```

      Can be utilized to get specific user accounts within Azure

### **2. Cloud Service Dashboard (**&#x54;153&#x38;**)**

* Attackers compromise credentials to access the Azure Portal and explore services.
  * **Example:** Logging into the Azure Portal using stolen credentials to navigate through subscriptions and resources, such as Virtual Machines or App Services.

### **3. Cloud Service Discovery:** **(T**152&#x36;**)**

* Attackers use CLI commands or APIs to discover active Azure services.
  *   **Example:** Using Azure CLI:

      ```bash
      az resource list --query "[].{name:name, type:type}" --output table
      ```

      This lists all resources and their types within a subscription​​.

### 4. **Password Policy Discovery**

* Attackers discover password policies in Entra ID to refine brute-force or credential attacks.
  *   **Example:** Using Entra PowerShell to retrieve the directory's password policy:

      ```powershell
      Get-MsolPasswordPolicy
      ```

      This reveals information about password complexity and expiration settings​​.

### 5. **Permission Groups Discovery (T1069)**

* **Cloud Groups:** Attackers enumerate Entra ID groups and their members to locate privileged roles.
  *   **Example:** Using Azure CLI to list groups:

      ```bash
      az ad group list --query "[].{Name:displayName, ID:id}" --output table
      ```

      This lists all groups within Entra ID.
  *   To enumerate group members:

      ```bash
      az ad group member list --group "GroupName" --query "[].{Name:displayName, UserPrincipalName:userPrincipalName}" --output table
      ```

      This retrieves the members of a specific Entra ID group​​.
