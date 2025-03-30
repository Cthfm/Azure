# Discovery TA00007

## Overview:

In Microsoft Azure Infrastructure-as-a-Service (IaaS), adversaries use discovery techniques (TA0007) to identify cloud resources and services that can be leveraged for further exploitation. These techniques help attackers enumerate virtual machines, networking components, storage accounts, and identity-related configurations to understand the environment. Often, reconnaissance efforts blend with legitimate administrative activities, making detection challenging. Implementing continuous monitoring, anomaly detection, and least-privilege access models is essential to mitigate these risks.

### **Account Discovery (T1087)**

Attackers attempt to enumerate users, groups, and permissions to understand the access hierarchy in an Azure environment.

#### **T1087.004 – Cloud Account Discovery**

* **Example Attack:**
  *   Using **Azure CLI** to list user accounts:

      ```powershell
      az ad user list --query "[].{Name:displayName, UserPrincipalName:userPrincipalName}"
      ```

### **Cloud Infrastructure Discovery (T1580)**

Attackers attempt to identify virtual machines, databases, and cloud resources in an Azure subscription.

* **Example Attack:**
  *   Using Azure CLI to list resources within a given tenant:

      <pre class="language-powershell"><code class="lang-powershell"><strong>az resource list --query "[].{Name:name, Type:type}
      </strong></code></pre>

### **Cloud Service Dashboard (T1590.001)**

Attackers may log into the Azure portal portal.azure.com to manually browse resources.

* **Example Attack:**
  * Login with stolen credentials and browse Resource Explorer.

### **Cloud Service Discovery (T1526)**

Attackers enumerate available Azure services and regions.

* **Example Attack:**
  *   Identifying cloud regions:

      ```powershell
      az account list-locations --query "[].{Region:name}"
      ```

### **Cloud Storage Object Discovery (T1613)**

Attackers scan for publicly accessible storage blobs.

* **Example Attack:**
  *   Listing storage containers:

      ```powershell
      az storage blob list --container-name mycontainer --account-name mystorage
      ```

### **Log Enumeration (T1005)**

Attackers attempt to access Azure logs to gather intel on security events.

* **Example Attack:**
  *   Retrieving logs from Azure Monitor:

      ```powershell
      az monitor activity-log list --max-items 10
      ```

### **Network Service Discovery (T1046)**

Attackers scan Azure virtual networks (VNets) and Network Security Groups (NSGs).

* **Example Attack:**
  *   Checking network security rules:

      ```powershell
      az network nsg rule list --resource-group MyResourceGroup --nsg-name MyNSG
      ```
  *   Performing internal network scanning:

      ```bash
      nmap -p- -Pn -T4 <Target-IP>
      ```

### **Network Sniffing (T1040)**

If an attacker gains control of a compromised Azure VM, they might attempt packet sniffing.

* **Example Attack:**
  *   Running `tcpdump` to capture traffic:

      ```bash
      tcpdump -i eth0 -w capture.pcap
      ```

### **Password Policy Discovery (T1201)**

Attackers query password policies to plan credential attacks.

* **Example Attack:**
  *   Retrieving Azure Entra ID password policy:

      ```powershell
      # Connect to Microsoft Graph
      Connect-MgGraph -Scopes "Policy.Read.All", "Directory.Read.All"

      # Get password policy info
      Get-MgPolicyAuthenticationMethodsPolicy
      ```

### **Permission Groups Discovery (T1069)**

Attackers enumerate **Azure Entra ID groups** to identify privileged accounts.

#### **T1069.003 – Cloud Groups Discovery**

* **Example Attack:**
  *   Listing Entra ID groups:

      ```powershell
      Get-EntraGroup 
      ```
  *   Checking role assignments:

      ```powershell
      az role assignment list --query "[].{Role:roleDefinitionName, User:principalName}"
      ```

### **Software Discovery (T1518)**

Attackers investigate security software and system configurations.

#### **T1518.001 – Security Software Discovery**

* **Example Attack:**
  * Check for installed security solutions:

**T1518.002 – System Information Discovery**

* **Example Attack:**
  *   Gathering system details:

      ```powershell
      az vm show --name myVM --resource-group myRG
      ```

#### **T1518.003 – System Location Discovery**

* **Example Attack:**
  *   Identifying VM locations:

      ```powershell
      az account list-locations
      ```

&#x20;**T1518.004 – System Network Connections Discovery**

* **Example Attack:**
  *   Checking active network connections:

      ```powershell
      netstat -ano
      ```
