# Credentialed Access TA00060

## Overview:

Attackers targeting Azure often aim to harvest or forge credentials to escalate privileges, move laterally, or maintain persistence. Below are key techniques and Azure-specific examples aligned with the MITRE ATT\&CK framework.

### Brute Force (T1110)

**Description:** Repeatedly attempt authentication using password-based methods.

**Password Guessing (T1110.001)**

**Azure Example:**\
Attempt login using a known username (`admin@tenant.onmicrosoft.com`) with common passwords via the Azure AD sign-in endpoint.

Use automated tools like Hydra or AADInternals to perform low-volume guessing to evade detection.

**Password Spraying (T1110.003)**

**Azure Example:**\
Spray a list of common passwords (e.g., `Winter2024!`) across many Azure AD accounts using `Invoke-AADIntSpray` (AADInternals).

Bypass account lockouts with low-and-slow attempts from rotating IPs.

**Credential Stuffing (T1110.004)**

**Azure Example:**\
Use previously leaked credentials from breaches to access Azure services like Outlook, Azure Portal, or Graph API.

Leverage tools like `MicroBurst`, `ROADtools`, or `FireProx` to automate login attempts while rotating IP addresses.

#### Credentials from Password Stores (T1555.006)

**Cloud Secrets Management Stores**\
**Description:** Access credentials stored in platforms like Azure Key Vault.

**Azure Example:**\
Exploit a misconfigured Function App or Automation Account to retrieve secrets from Key Vault using `DefaultAzureCredential()`:

```python
from azure.keyvault.secrets import SecretClient
secret_client = SecretClient(vault_url="https://myvault.vault.azure.net", credential=DefaultAzureCredential())
secret = secret_client.get_secret("sql-password")
```



### Forge Web Credentials (T1606)

**Description:** Forge authentication artifacts such as tokens or cookies.

**Web Cookies (T1606.001)**

**Azure Example:**\
Use a stolen Azure Portal session cookie (e.g., `x-ms-cpim-trans`) to impersonate a logged-in user.

Replay the session in a browser or through custom HTTP tooling (e.g., Burp, Fiddler).

**SAML Tokens (T1606.002)**

**Azure Example:**\
Forge or manipulate a SAML token used in Azure AD federated login flows (e.g., exploiting misconfigured ADFS).

***

### Modify Authentication Process (T1556)

**Description:** Alter authentication mechanisms to weaken or bypass identity protections.

**Multi-Factor Authentication (T1556.006)**

**Azure Example:**\
Exploit MFA fatigue by sending repeated push notifications using `MSGraphNotifications` or `AADInternals` until the user accepts.

**Hybrid Identity (T1556.007)**

**Azure Example:**\
Compromise on-prem AD, then sync forged identities into Azure Entra via Azure Entra Connect.

Abuse unsynced password changes or misconfigured sync scopes to inject malicious accounts.

**Conditional Access Policies (T1556.008)**

**Azure Example:**\
Use a privileged identity to modify Conditional Access policies, excluding attacker IPs or device types from MFA or location checks:

```bash
az rest --method PATCH --uri https://graph.microsoft.com/v1.0/identity/conditionalAccess/policies/{policy-id}
```

### Network Sniffing (T1040)

**Description:** Capture network traffic from within a compromised Azure VM to steal credentials.

**Azure Example:**\
Use `tcpdump` or `Wireshark` on a Linux VM to capture unencrypted HTTP Basic Auth or LDAP traffic.

Capture authentication headers from misconfigured internal services or during a phishing C2 callback.

```bash
tcpdump -i eth0 port 80 or port 443 -w creds.pcap
```

### Steal Application Access Token (T1528)

**Description:** Use a stolen access token to impersonate a user or service.

**Azure Example:**\
Extract Bearer token from browser DevTools or logs and use it to call Microsoft Graph:

```http
GET https://graph.microsoft.com/v1.0/me
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJh...
```

Leverage this token to access email, files, calendars, or administrative APIs depending on token scope.

### Unsecured Credentials (T1552)

**Description:** Steal credentials stored insecurely in files or metadata.

**Credentials in Files (T1552.001)**

**Azure Example:**\
Search deployed Function Apps, DevOps pipelines, or containers for hardcoded secrets in:

* `local.settings.json`
* `.env`
* `web.config`

```bash
grep -i 'password\|key\|secret' -R .
```

**🔹 Cloud Instance Metadata API (T1552.006)**

**Azure Example:**\
Query the Azure Instance Metadata Service (IMDS) from a compromised VM to extract a token:

```bash
curl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?resource=https://management.azure.com&api-version=2018-02-01"
```

Use token to impersonate the VM’s managed identity and access other Azure resources (e.g., Key Vault, Storage).
