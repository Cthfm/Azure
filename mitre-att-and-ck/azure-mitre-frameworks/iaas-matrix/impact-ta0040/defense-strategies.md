# Defense Strategies

## Defensive Strategies Against Impact in Azure

Disruptive impact techniques in Microsoft Azure can lead to data loss, service outages, and long-term operational setbacks. Defending against TA0040 – Impact requires a multi-layered approach combining identity protection, data resilience, recovery assurance, and proactive monitoring.

### 1️⃣ Access Control & Recovery Resilience _(T1531, T1490)_

**Harden Privileged Access and Protect Recovery Systems**

* Enforce Just-in-Time access via Azure Entra ID Privileged Identity Management (PIM) for backup admins and Key Vault contributors.
*   Audit and alert on sudden removal of role assignments or service principal deletions:

    ```powershell
    Get-AzRoleAssignment | Where-Object {$_.RoleDefinitionName -eq "Contributor"}
    ```
* Implement MFA + Conditional Access for all admin accounts.
*   Prevent Key Vault deletion using Soft Delete and Purge Protection:

    ```bash
    az keyvault update --name <vault> --enable-soft-delete true --enable-purge-protection true
    ```
* Restrict access to Recovery Services Vaults and monitor backup job deletion attempts.

### 2️⃣ Data Encryption & Recovery Protection _(T1486, T1490)_

**Prevent Unauthorized Encryption and Ensure Recoverability**

* Enforce Key Vault RBAC and restrict access to customer-managed keys (CMKs).
* Detect and alert on unauthorized key rotations or deletions.
* Enable Azure Backup with immutable vault settings (WORM lock) for critical workloads.
* Regularly test recovery of VMs, databases, and storage to ensure backup integrity.
* Configure long-term retention and prevent automated policy overrides.

### 3️⃣ Denial of Service Mitigation _(T1498.001, T1498.002, T1499.001, T1499.002, T1499.003)_

**Protect Azure Services from Resource and Application Exhaustion**

* Enable Azure DDoS Protection Standard for public-facing resources.
* Use rate limiting and throttling for APIs hosted in App Services or Azure Functions.
* Apply WAF (Web Application Firewall) rules to mitigate Layer 7 attacks.
* Implement NSG and Azure Firewall rules to:
  * Block inbound UDP floods (T1498.001)
  * Detect DNS or NTP reflection patterns (T1498.002)
  * Log high-throughput HTTP requests to Function Apps (T1499.002)
* Use Sentinel + Network Watcher to alert on sudden spikes in inbound traffic.

### 4️⃣ Data Integrity & Web Resource Protection _(T1491.001)_

**Secure Azure Web Apps and Prevent Defacement**

* Enforce CI/CD pipeline security: scan for secrets, enforce code reviews, and lock deployment sources.
* Disable FTP/FTPS deployment in App Services and use Azure DevOps or GitHub Actions with managed identities.
* Enable App Service File Change Audit Logging to detect unexpected file replacements.
* Restrict write access to blob containers used for static website hosting.
* Use MCAS or Defender for Cloud Apps to detect changes to externally accessible content.

### 5️⃣ Resource Abuse & Hijacking Prevention _(T1496.001, T1496.002)_

**Prevent Compute and Bandwidth Hijacking**

* Use Azure Policy to restrict creation of VM SKUs often used for cryptomining.
* Monitor for unusual process activity in VMs using Microsoft Defender for Endpoint (e.g., miner binaries).
* Detect anomalous egress traffic patterns to mining pools or TOR relays using NSG Flow Logs.
* Limit outbound traffic to trusted IPs or FQDNs via Azure Firewall.
* Alert on unauthorized container deployments in ACR or AKS that consume high CPU or bandwidth.

### 📌 Summary Table of Defensive Strategies for TA0040 – Impact

| Category                             | Related Techniques            | Key Defensive Controls                                         |
| ------------------------------------ | ----------------------------- | -------------------------------------------------------------- |
| Access Control & Recovery Resilience | T1531, T1490                  | PIM, Role Auditing, Soft Delete, MFA                           |
| Data Encryption & Backup Protection  | T1486, T1490                  | Key Vault RBAC, Immutable Backups, Key Rotation Alerts         |
| Denial of Service Protections        | T1498.001, T1498.002, T1499.x | DDoS Standard, WAF, Rate Limits, Firewall Rules                |
| Web App & Static Site Protection     | T1491.001                     | CI/CD Hardening, Deployment Restrictions, File Change Auditing |
| Resource Hijacking Mitigation        | T1496.001, T1496.002          | Defender for Endpoint, Egress Monitoring, Azure Policy         |
