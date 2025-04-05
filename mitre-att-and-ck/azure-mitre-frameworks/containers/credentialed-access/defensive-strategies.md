# Defensive Strategies

## **Defensive Strategies Against Credentialed Access in Containerized Environments**

Credentialed Access techniques involve adversaries using valid accounts, secrets, tokens, or certificates to gain access without triggering alarms. In Kubernetes and container ecosystems, weak credentials, leaked tokens, and mismanaged secrets make this easy for attackers.\
Your goal is to secure identities, harden secrets management, and monitor authentication flows.

### 1. **Enforce Strong Authentication and Identity Controls**

| Action                                                                  | Why It Matters                                        |
| ----------------------------------------------------------------------- | ----------------------------------------------------- |
| Integrate Kubernetes API authentication with Azure Entra ID/OIDC (SSO)  | Strong cloud identities reduce password-based attacks |
| Rotate Kubernetes ServiceAccount tokens periodically                    | Shorten token lifetime to minimize risk if stolen     |
| Use workload identity (Azure/GKE/AWS) instead of static secrets in pods | Tokens expire dynamically, hard to abuse              |
| Disable or delete default Kubernetes ServiceAccounts                    | Default accounts are often over-privileged targets    |

Protects against valid account techniques and alternative authentication material.&#x20;

### 2. **Protect Secrets and Credentials at Rest**

| Action                                                                                           | Why It Matters                                        |
| ------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| Encrypt Kubernetes Secrets at rest using KMS providers (Azure Key Vault, HashiCorp Vault)        | Secrets aren't stored in plaintext in etcd            |
| Avoid storing secrets in environment variables or configmaps                                     | Environment variables are often exposed accidentally  |
| Use sealed secrets, external secret managers, or CSI drivers                                     | Secrets are pulled on demand and harder to steal      |
| Continuously scan images, repos, and file systems for exposed secrets (`trufflehog`, `gitleaks`) | Prevent accidental leakage in codebases or containers |

Prevents  Unsecured Credentials in Files/Container APIs.

***

### 3. **Defend Against Brute Force and Password Guessing**

| Action                                                                                      | Why It Matters                                               |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Require MFA (Multi-Factor Authentication) for Kubernetes dashboards and cloud portal access | Brute force attacks are useless against MFA                  |
| Lock down APIs with rate limiting (e.g., nginx Ingress, API Gateway)                        | Throttle brute force login attempts                          |
| Monitor for multiple failed login attempts across Kubernetes and cloud auth logs            | Early detection of password guessing and credential stuffing |
| Disable basic authentication for Kubernetes API server (use tokens/certs only)              | No username/password brute force paths                       |

Protects against brute force activities.&#x20;

***

### 4. **Restrict Service Account and Metadata API Access**

| Action                                                                                     | Why It Matters                   |
| ------------------------------------------------------------------------------------------ | -------------------------------- |
| Set `automountServiceAccountToken: false` by default on pods                               | No automatic credential exposure |
| Protect access to Azure/GCP/AWS Instance Metadata APIs (IMDS) with egress network policies | Block token theft from pods      |
| Require IAM Role scoping for pods via Workload Identity or Azure AD Pod Identities         | Fine-grained cloud access        |

Defends against Application stealling

***

### 5. **Monitor Credential Usage and Token Abuse**

| Action                                                                                                                              | Why It Matters                                    |
| ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| Enable Kubernetes audit logs and monitor access to Secrets and ServiceAccounts                                                      | Detect unexpected secret reads                    |
| Deploy Falco rules to catch suspicious use of `kubectl get secrets`, `curl` to metadata APIs, or mass reads from `/var/run/secrets` | Live runtime threat detection                     |
| Centralize logging of cloud login attempts (Azure SignIn Logs, GCP IAM logs, AWS CloudTrail)                                        | Cloud-wide visibility on credential use and abuse |

Gives real-time monitoring for credential access behaviors.

***

### Defensive Coverage Table (Credentialed Access)

| Attack Vector                     | Defensive Strategy                                       |
| --------------------------------- | -------------------------------------------------------- |
| Default Service Accounts          | Disable defaults, enforce strong ServiceAccount controls |
| Stolen Tokens                     | Protect IMDS access, rotate tokens, workload identities  |
| Weak Passwords                    | Use SSO, MFA, strong password policies                   |
| Secrets in Files                  | Encrypt secrets, externalize secret storage              |
| Brute Force / Credential Stuffing | Rate limit, alert on login anomalies, enforce MFA        |

***

## Final Summary

Defending against Credentialed Access focuses on:

* **Hardening identities and authentication** (passwordless, token rotation, MFA)
* **Securing secrets and tokens** (encryption, minimal exposure)
* **Detecting brute force and abuse early** (audit logs + Falco runtime detection)
* **Blocking abuse of cloud metadata services** (lock down pod egress)
