# Impact TA0040

## Overview:

In Microsoft Azure, adversaries use Impact techniques to disrupt availability, destroy data, and impair recovery. This includes removing access to critical accounts (T1531), triggering auto-deletion through storage or backup policies (T1485.001), encrypting cloud data with unauthorized keys (T1486), and defacing publicly hosted apps (T1491.001). Denial-of-service attacks can target applications or network infrastructure through flooding or amplification (T1498, T1499), while recovery is hindered by deleting backups or purging Key Vaults (T1490). Attackers may also hijack Azure compute or bandwidth for crypto mining or proxy abuse (T1496), turning cloud resources into liabilities. These risks emphasize the need for strong access control, resilient recovery configurations, and continuous monitoring.

### **Account Access Removal (T1531)**

**Description:** Adversaries remove legitimate users from access to disrupt operations or cover tracks.

#### Azure Example:

* Use stolen privileges to remove users from Azure Entra ID groups or delete role assignments:

```bash
az role assignment delete --assignee <user> --role Contributor
```

* Disable service principals or Managed Identities to break automation.
* Remove admins from Key Vault access policies to block recovery:

```bash
az keyvault set-policy --name myvault --object-id <admin-id> --clear-permissions-all
```

### **Data Destruction (T1485)**

#### Lifecycle-Triggered Deletion (T1485.001)

**Description:** Leverage resource lifecycles to delete or auto-expire data.

#### Azure Example:

* Abuse Azure Storage Lifecycle Policies to auto-delete blobs after X days:

```json
"actions": {
  "baseBlob": {
    "delete": { "daysAfterModificationGreaterThan": 0 }
  }
}
```

* Modify Azure Backup retention policies to cause backup deletion and prevent recovery.
* Schedule auto-delete for secrets in Key Vault or purge soft-deleted vaults:

```bash
az keyvault purge --name myvault
```

### **Data Encrypted for Impact (T1486)**

**Description:** Encrypt data at rest or in transit to make it unusable to the target.

**Azure Example:**

* Use a compromised Function App or Automation Account to encrypt all blob storage files with an unknown key.
* Rotate the Key Vault encryption key for storage accounts, locking out the original key:

```bash
az keyvault key rotate --vault-name myvault --name storage-key
```

* Apply a new customer-managed key (CMK) to encrypted resources and destroy the original key.

### **Defacement (T1491)**

#### External Defacement (T1491.001)

**Description:** Modify externally visible resources like websites or public-facing services.

#### Azure Example:

* Replace Azure App Service or static website content:

```bash
az webapp deployment source config-zip --src defaced.zip --name victimweb
```

* Overwrite index.html in Azure Blob Static Website Hosting with malicious/defaced content.

### **Endpoint Denial of Service (T1499)**

**Description:** Exhaust endpoint resources to make systems unresponsive.

#### Service Exhaustion Flood (T1499.001)

Azure Example:

* Use multiple bots or VMs to flood an Azure App Service or API endpoint, maxing out outbound connections or CPU.

#### Application Exhaustion Flood (T1499.002)

Azure Example:

* Hit a Function App or Logic App endpoint with malformed data at high volume to exhaust runtime or threading limits.
* Bombard Azure-hosted APIs with large payloads or deep object nesting (DoS logic flaw).

#### Application or System Exploitation (T1499.003)

Azure Example:

* Exploit an unpatched App Service vulnerability to cause a crash.
* Abuse a vulnerability in an Azure VM-based application (e.g., buffer overflow in a public app) to take down the system.

### **Inhibit System Recovery (T1490)**

Description: Interfere with backup or recovery mechanisms to prevent rollback.

#### Azure Example:

* Delete Azure Recovery Vault backups or reduce retention:

```bash
az backup item delete --vault-name MyVault --container-name MyContainer --name VM1
```

* Revoke backup operator access or disable Recovery Services Vault backup jobs.
* Purge soft-deleted Key Vaults, preventing key recovery:

```bash
az keyvault purge --name myvault
```

***

### **Network Denial of Service (T1498)**

#### Direct Network Flood (T1498.001)

**Description:** Flood a target directly with packets to overwhelm resources.

Azure Example:

* Use a botnet or attacker-controlled Azure VMs to flood a Load Balancer, Azure Firewall, or App Gateway with SYN/UDP/ICMP traffic.
* Target VM public IP with UDP floods until the VM’s bandwidth quota is exceeded.

#### Reflection Amplification (T1498.002)

**Description:** Use third-party systems to reflect and amplify attack traffic.

#### Azure Example:

* Abuse open Azure-hosted DNS or NTP services to reflect traffic toward a target system.
* Compromise an Azure VM and use it to relay spoofed requests to amplify DDoS toward another tenant or external IP.

### **Resource Hijacking (T1496)**

#### Compute Hijacking (T1496.001)

**Description:** Steal compute resources for cryptomining or unauthorized use.

#### Azure Example:

* Deploy crypto-mining malware to Azure VMs or container apps.
* Abuse a compromised Azure DevOps pipeline to run hidden compute tasks.

#### Bandwidth Hijacking (T1496.002)

**Description:** Use an organization’s bandwidth for malicious activity.

#### Azure Example:

* Use an Azure VM to exfiltrate large datasets or host C2/illegal content, consuming egress bandwidth.
* Deploy TOR relays or proxy tunnels on Azure App Services or VMs to anonymize attacker traffic at the victim’s expense.
