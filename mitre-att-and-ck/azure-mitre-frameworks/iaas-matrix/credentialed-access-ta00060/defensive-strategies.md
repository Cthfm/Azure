# Defensive Strategies

## Credentialed Access Defensive Strategies

Credential theft in Microsoft Azure can enable adversaries to bypass authentication, impersonate users, escalate privileges, and persist silently. Defending against TA0006 – Credential Access requires a layered defense combining identity hardening, token protection, logging, and privileged access governance.

### 1️⃣ Identity Hardening & Authentication Security _(T1110, T1556.006, T1556.008, T1552.001)_

**Strengthen Authentication and Limit Brute Force Exposure**

* Enforce Multi-Factor Authentication (MFA) for all users, especially privileged and cloud resource admins.
* Configure Azure AD Smart Lockout to prevent brute force attempts and password spraying.
* Implement password protection policies using Azure AD Password Protection to block common terms and leaked passwords.
* Audit risky sign-ins via Microsoft Entra Sign-In Logs and sign-in frequency to detect abnormal patterns.
* Disable legacy authentication protocols (e.g., IMAP, POP, SMTP Basic) via Conditional Access.
* Rotate hardcoded credentials found in code or `local.settings.json`. Use Managed Identity instead.

### 2️⃣ Secrets & Token Protection _(T1555.006, T1552.006, T1528)_

**Secure Access Tokens, Secrets, and Metadata APIs**

* Enable Azure Key Vault RBAC and audit Key Vault access via Diagnostic Logs.
* Use Managed Identity and `DefaultAzureCredential()` for apps — avoid embedded secrets.
* Deny public access to managed identity endpoints on VMs, containers, and App Services.
*   Prevent token theft from the Instance Metadata Service (IMDS) by disabling unnecessary access:

    ```bash
    az vm identity remove --resource-group <rg> --name <vm>
    ```
* Set short token lifetimes for OAuth access tokens and monitor Graph API token usage in Azure Sentinel.
* Use App Registration permissions sparingly — review token scopes regularly.

#### 3️⃣ Web Credential Forgery & Session Protection _(T1606.001, T1606.002, T1528)_

**Detect and Block Session Replay & Token Abuse**

* Enable Continuous Access Evaluation (CAE) to invalidate tokens after risky events.
* Prevent SAML token forgery by enforcing secure signing practices and rotating SSO certificates.
* Use Microsoft Defender for Cloud Apps to detect impossible travel or improbable session usage from multiple IPs.
* Restrict cookie lifetime via Azure AD session settings.
* Use Sign-in frequency policies to enforce re-authentication after short durations (e.g., 8 hours).
* Detect unusual API token usage with Azure Sentinel KQL queries

#### 4️⃣ Brute Force & Password Attack Prevention _(T1110.001, T1110.003, T1110.004)_

**Prevent Account Lockout Bypass and Password Spray**

* Monitor failed sign-ins with Microsoft Sentinel and alert on failed attempts from multiple IPs.
* Create Conditional Access policies that block sign-ins from legacy clients.
* Apply sign-in risk policies in Entra ID to block high-risk authentications.
* Block attackers from cycling through accounts by enforcing Smart Lockout, setting threshold of 10 with 60s lock duration.
* Use Defender for Identity (formerly Azure ATP) to detect on-prem password guessing that syncs to Azure.

#### 5️⃣ Credential Hygiene & Code Scanning _(T1552.001, T1552.006)_

**Prevent Exposure of Secrets in Files, Pipelines, and Metadata**

* Integrate Microsoft Defender for DevOps or tools like `TruffleHog`, `Gitleaks` into CI/CD pipelines.
*   Regularly scan deployed Azure Functions, containers, and App Service code for embedded secrets:

    ```bash
    grep -i 'password\|apikey\|token' -R .
    ```
* Remove long-lived credentials and enforce use of short-lived access tokens.
* Monitor file systems on VMs and App Services for config files containing secrets.
* Audit `local.settings.json` and `.env` files in source repos for hardcoded secrets.
* Restrict access to container metadata APIs and protect against IMDS-based token theft.

***

### 📌 Summary Table of Defensive Strategies for TA0006 – Credential Access

| Category                            | Related Techniques                     | Key Defensive Controls                                        |
| ----------------------------------- | -------------------------------------- | ------------------------------------------------------------- |
| Identity Hardening & Authentication | T1110, T1556.006, T1556.008, T1552.001 | MFA, Smart Lockout, Password Policy, Conditional Access       |
| Secrets & Token Protection          | T1555.006, T1552.006, T1528            | Managed Identity, Token Audit, Key Vault RBAC                 |
| Web Credential & Session Protection | T1606.001, T1606.002, T1528            | CAE, Sign-in Frequency, Token Lifetime, SSO Security          |
| Brute Force Attack Prevention       | T1110.001, T1110.003, T1110.004        | Entra Smart Lockout, Risk-Based Access, Defender for Identity |
| Credential Hygiene & Code Scanning  | T1552.001, T1552.006                   | Code Scanning, DevOps Security, File Monitoring               |
