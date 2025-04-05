# Initial Access TA0001

## **Initial Access Techniques in Azure Environments**

In Microsoft Azure, adversaries use Initial Access techniques to establish an entry point into cloud environments. This includes exploiting public-facing applications (e.g., App Services, APIs, AKS workloads), abusing misconfigured trusted relationships (e.g., cross-tenant access, B2B collaboration), and leveraging valid but weak credentials (default, cloud admin accounts).\
Successful Initial Access enables attackers to deploy resources, steal secrets, or move laterally within Azure subscriptions and connected services.

***

### Exploit Public-Facing Application **(T1190)**

**Description**:\
Exploit vulnerabilities in publicly accessible Azure services such as Web Apps (App Services), Azure Kubernetes Service (AKS), APIs behind Application Gateways, or exposed VMs to gain unauthorized access.

**Azure Example**:\
An attacker exploits an unpatched Azure App Service (web app) vulnerability:

```bash
# Exploit an RCE vulnerability on a public Azure Web App
curl -X POST https://victim-app.azurewebsites.net/vulnerable-endpoint -d 'payload=malicious code'
```

Upon successful exploitation, the attacker gains a web shell or remote code execution within the app’s environment, allowing them to pivot deeper into the Azure environment, access managed identities, or exfiltrate storage account keys.

***

### Trusted Relationship **(T1199)**

**Description**:\
Abuse misconfigured or overly permissive trusted connections between Azure tenants, subscriptions, or B2B federated identities to access Azure resources.

**Azure Example**:\
An attacker leverages a compromised account from a trusted external Azure Entra ID tenant to access internal resources:

```bash
# Use an external user invite (B2B) to access a sensitive Azure subscription
az login --username compromised_user@trustedtenant.com
az account list --all
```

Because the external user has been given Contributor or Owner roles in the target subscription (common in poor B2B setups), the attacker can deploy, modify, or exfiltrate Azure resources.

***

### Valid Accounts T1078

**Description:**

Valid Accounts refers to adversaries gaining access by using legitimate credentials instead of exploiting vulnerabilities.\
Rather than breaking the door down, attackers use the real keys — compromised usernames, passwords, API keys, service principals, or certificates — to log into Azure environments as trusted users or services.

In Azure IaaS environments, this typically includes:

* Using stolen Azure Active Directory (Entra ID) user credentials
* Using compromised SSH private keys to access VMs
* Abusing Azure Service Principals or Managed Identity tokens
* Reusing default credentials (e.g., unchanged admin/admin accounts)

Attackers leveraging valid accounts can bypass many security controls like MFA (if not enforced properly) and move silently, appearing as normal users or systems.

#### **Default Accounts T1078.001**

**Description**:\
Use known or default Azure accounts, service principals, managed identities, or credentials with weak configurations to gain access without needing exploitation.

**Azure Example**:\
An attacker finds and abuses a default Azure service principal used for automation, which still has the original client secret and is over-privileged:

```bash
# Authenticate using a known leaked client ID and secret
az login --service-principal -u <client-id> -p <client-secret> --tenant <tenant-id>
```

This allows access to Azure Resource Manager (ARM) APIs, where they can deploy VMs, exfiltrate storage, or manipulate configurations.

***

### Valid Accounts T1078

**Description**

Valid Accounts refers to adversaries gaining access to systems, networks, or cloud environments by using legitimate, authorized credentials.\
Rather than exploiting vulnerabilities or dropping malware, attackers log in just like any authorized user would blending perfectly into normal operations.

Valid account use includes:

* Usernames and passwords (stolen, guessed, or leaked)
* SSH private keys
* API keys
* OAuth tokens
* Service account credentials
* Session cookies

Because these credentials are valid, most systems see the attacker as a legitimate user, making detection far more difficult compared to traditional intrusion methods.

#### **Cloud Accounts** T1078.004

**Description**:\
Use valid Entra ID credentials (user accounts, service principals, managed identities) obtained through phishing, leaks, or previous breaches to authenticate directly into Azure services.

**Azure Example**:\
An attacker uses stolen cloud credentials obtained through a phishing campaign:

```bash
# Login interactively as a legitimate Azure AD user
az login --username stolenuser@victimdomain.com
```

After logging in, the attacker enumerates Azure subscriptions:

```bash
az account list --output table
```

Then pivots into sensitive services like Azure Key Vault, Storage Accounts, or Defender settings to escalate privileges or establish persistence.

***

## 📊 Summary Table

| Technique/Subtechnique            | MITRE ID      | Azure Example                                                                    |
| --------------------------------- | ------------- | -------------------------------------------------------------------------------- |
| Exploit Public-Facing Application | **T1190**     | Exploit an RCE vulnerability in Azure App Services, APIs, AKS, exposed VMs       |
| Trusted Relationship              | **T1199**     | Abuse external tenant B2B trust or misconfigured cross-tenant access             |
| Valid Accounts → Default Accounts | **T1078.004** | Use default Azure service principals, managed identities, or automation accounts |
| Valid Accounts → Cloud Accounts   | **T1078.004** | Use valid Azure Entra ID credentials obtained via phishing, leaks, or compromise |

***

## 🎯 Final Summary

Defending against Initial Access in Azure requires:

* **Patching public-facing services regularly** (App Services, AKS, APIs)
* **Tightly controlling trusted external user access** (B2B, Cross-tenant trust)
* **Rotating and securing service principals and client secrets**
* **Hardening cloud identity management with MFA, Conditional Access, and threat detection**

