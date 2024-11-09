# Defensive Strategies: TA0007

## **Defensive Strategies for TA0007 - Discovery**

The **Discovery (TA0007)** tactic involves attackers gathering **critical information about accounts, networks, configurations, and resources** to plan their next moves. Defending against these reconnaissance efforts in **Azure** requires **monitoring, hardening configurations, and restricting permissions** to minimize data exposure.

### **1. Monitor and Restrict Account and Group Discovery**

**Mitigates:** T1087 - Account Discovery, T1069 - Permission Groups Discovery

* **Action:** Prevent attackers from enumerating users, roles, and permissions.
* **Azure Procedure:**
  * Use **Role-Based Access Control (RBAC)** to restrict permissions for accessing user and group information.
  * Monitor **Azure AD audit logs** for queries targeting **user or group listings**.
  *   Enable **Azure Sentinel alerts** to detect unauthorized API calls, such as:

      ```bash
      az ad user list --output table
      ```
  * Use **Azure AD Privileged Identity Management (PIM)** to limit privileged roles like **Global Administrator**.

### **2. Harden Metadata Services to Prevent Token Theft**

**Mitigates:** T1552.004 - Credentials in Cloud Metadata

* **Action:** Secure **Azure Instance Metadata Service (IMDS)** to prevent attackers from retrieving tokens.
*   **Azure Procedure:**

    * Use **Network Security Groups (NSGs)** to restrict access to IMDS.
    * Monitor for IMDS access using **Azure Defender for VMs** and **Azure Sentinel**.
    * Disable unnecessary outbound access to **169.254.169.254** (IMDS IP).

    ```bash
    curl -H "Metadata: true" http://169.254.169.254/metadata/identity/oauth2/token
    ```

### **3. Restrict Permissions for Network and System Discovery**

**Mitigates:** T1016 - System Network Configuration Discovery, T1018 - Remote System Discovery

* **Action:** Limit access to **VNet and NSG configurations** to prevent unauthorized network mapping.
* **Azure Procedure:**
  * Apply **RBAC policies** to restrict access to virtual network and peering configuration.
  * Monitor **NSG rule changes** with **Azure Monitor**.
  * Use **Azure Policy** to enforce best practices for **network segmentation** and **restricted peering**.
  *   Set alerts for commands like:

      ```bash
      az network vnet peering list --output table
      ```

### **4. Monitor and Audit Role and Permission Assignments**

**Mitigates:** T1069.002 - Domain Groups Discovery

* **Action:** Regularly audit **role assignments and group memberships** to detect privilege escalation paths.
* **Azure Procedure:**
  * Use **Azure AD PIM** to limit and monitor changes to **privileged roles**.
  * Configure **Azure Sentinel alerts** for new role assignments.
  *   Regularly review **role assignments** with commands like:

      ```bash
      az role assignment list --output table
      ```

### **5. Detect and Block Automated Service Enumeration**

**Mitigates:** T1057 - Process Discovery

* **Action:** Monitor for **automated enumeration** of VMs, databases, and storage accounts.
* **Azure Procedure:**
  * Use **Azure Monitor** and **Sentinel** to detect bulk resource listing.
  *   Set alerts for suspicious API queries:

      ```bash
      az vm list --output table
      az sql server list --output table
      ```
  * Apply **RBAC** to limit which users can view resource details.

### **6. Monitor Automation Accounts and Runbook Modifications**

**Mitigates:** T1083 - File and Directory Discovery

* **Action:** Track changes to **automation accounts and runbooks** to prevent abuse.
* **Azure Procedure:**
  * Monitor **Azure Automation logs** for suspicious activity involving runbook modifications.
  *   Use **Sentinel alerts** for unauthorized access to automation tasks:

      ```bash
      az automation runbook list --output table
      ```
  * Limit automation account permissions using **RBAC**.

### **7. Detect Security Tool Enumeration Attempts**

**Mitigates:** T1518 - Software Discovery

* **Action:** Monitor for **queries targeting security tools and configurations**.
* **Azure Procedure:**
  * Use **Azure Sentinel** to detect API queries related to security configurations.
  *   Set alerts for changes in **Azure Defender for Cloud** or monitoring agents:

      ```bash
      az security pricing list --output table
      az vm extension list --query "[?type=='Microsoft.Azure.Monitoring.Agent']" --output table
      ```
  * Ensure security tools cannot be disabled by unauthorized users through **RBAC**.

### **8. Use Just-in-Time (JIT) VM Access**

**Mitigates:** T1018 - Remote System Discovery

* **Action:** Apply **JIT access** to reduce the attack surface for **VM enumeration and remote system discovery**.
* **Azure Procedure:**
  * Enable **JIT access** in **Defender for Cloud** to limit access windows for RDP and SSH.
  * Monitor **Azure Activity Logs** for unauthorized attempts to access VMs.

### **9. Detect and Respond to VNet Peering Discovery Attempts**

**Mitigates:** T1016 - System Network Configuration Discovery

* **Action:** Monitor for **VNet peering enumeration** that may indicate reconnaissance.
* **Azure Procedure:**
  * Use **Azure Monitor** to track VNet peering queries.
  *   Set alerts for suspicious commands like:

      ```bash
      az network vnet peering list --output table
      ```

***

### **10. Automate Incident Response with Sentinel Playbooks**

**Mitigates:** Multiple Discovery Techniques

* **Action:** Use **automated playbooks** to respond to suspicious discovery attempts.
* **Azure Procedure:**
  * Configure **Azure Sentinel playbooks** to disable compromised accounts or block IPs in real-time.
  * Set playbooks to trigger on API calls involving:
    * Bulk listing of users or groups
    * Unauthorized role changes
    * Enumeration of network and security configurations

***

### **Summary of Defensive Procedures for TA0007**

| **Defensive Strategy**                | **Mitigates**                                  | **Azure Procedure**                                      |
| ------------------------------------- | ---------------------------------------------- | -------------------------------------------------------- |
| Monitor Account and Group Discovery   | T1087 - Account Discovery                      | Track API calls for user and group enumeration           |
| Harden Metadata Services              | T1552.004 - Credentials in Cloud Metadata      | Use NSGs to block unauthorized IMDS access               |
| Limit Network Discovery               | T1016 - System Network Configuration Discovery | Apply RBAC to restrict VNet access                       |
| Audit Role and Permission Assignments | T1069 - Permission Groups Discovery            | Use PIM and Sentinel to monitor role changes             |
| Detect Automated Resource Enumeration | T1057 - Process Discovery                      | Monitor resource listing commands with Azure Sentinel    |
| Monitor Automation Tasks and Runbooks | T1083 - File and Directory Discovery           | Track automation account modifications using Monitor     |
| Detect Security Tool Enumeration      | T1518 - Software Discovery                     | Use Sentinel to monitor queries targeting security tools |
| Use JIT Access for VMs                | T1018 - Remote System Discovery                | Apply JIT access in Defender for Cloud                   |
| Monitor VNet Peering Queries          | T1016 - System Network Configuration Discovery | Track peering queries with Azure Monitor                 |
| Automate Incident Response            | Multiple Discovery Techniques                  | Use Sentinel playbooks for real-time response            |
