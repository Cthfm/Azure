# Credentialed Access TA00060

**Credential Access Techniques in Azure Environments**

In Microsoft Azure, adversaries use Credential Access techniques to steal, forge, or brute-force credentials. Successful credential access allows lateral movement, privilege escalation, and persistence inside cloud environments.\
Credential attacks often focus on **passwords, cloud tokens, API secrets, or metadata services**.

***

#### 🔑 Brute Force → **T1110**

***

**➡️ Password Guessing**

\| MITRE ID | **T1110.001** |

**Description**:\
Systematically guess Azure user passwords to gain unauthorized access.

**Azure Example**:\
Attempt to log in using common passwords across Azure AD accounts:

```bash
bashCopyEditaz login --username victim@domain.com --password "Password123!"
```

✅ **Result**: Simple guessing against Azure AD accounts.

***

**➡️ Password Spraying**

\| MITRE ID | **T1110.003** |

**Description**:\
Attempt a few commonly used passwords across many Azure AD users to avoid account lockouts.

**Azure Example**:\
Spray "Welcome123!" against hundreds of Azure AD user accounts.

✅ **Result**: Mass guessing without triggering lockouts.

***

**➡️ Credential Stuffing**

\| MITRE ID | **T1110.004** |

**Description**:\
Use credential dumps (usernames/passwords from breaches) to try logging into Azure cloud services.

**Azure Example**:\
Replay stolen Office 365 credentials against Azure AD.

✅ **Result**: Takeover if reused passwords are still valid.

***

#### 🔐 Credentials from Password Stores → **Cloud Secrets Management Stores**

\| MITRE ID | **T1555.004** |

**Description**:\
Steal secrets directly from Azure Key Vault or AWS Secrets Manager equivalents.

**Azure Example**:\
Access Azure Key Vault if Service Principal is compromised:

```bash
bashCopyEditaz keyvault secret list --vault-name victim-vault
```

✅ **Result**: Immediate access to API keys, database credentials, etc.

***

#### 🛠️ Forge Web Credentials

***

**➡️ Web Cookies**

\| MITRE ID | **T1606.003** |

**Description**:\
Steal or forge Azure Portal web session cookies for access without authentication.

**Azure Example**:\
Use stolen session cookie to access Azure Portal directly without needing credentials.

✅ **Result**: Hijack authenticated sessions.

***

**➡️ SAML Tokens**

\| MITRE ID | **T1606.002** |

**Description**:\
Forge or steal SAML tokens to impersonate Azure users in federated SSO environments.

**Azure Example**:\
Use Golden SAML attack to impersonate an Azure AD user.

✅ **Result**: Complete federation bypass, invisible logins.

***

#### 🛡️ Modify Authentication Process

***

**➡️ Multi-Factor Authentication**

\| MITRE ID | **T1556.006** |

**Description**:\
Disable or weaken MFA settings in Azure Conditional Access to bypass additional verification.

**Azure Example**:

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --state disabled
```

✅ **Result**: Easier reentry and credential use.

***

**➡️ Hybrid Identity**

\| MITRE ID | **T1556.007** |

**Description**:\
Abuse Azure AD Connect synchronization to forge or hijack credentials between on-premises and cloud.

✅ **Result**: Stealthy cross-domain persistence.

***

**➡️ Conditional Access Policies**

\| MITRE ID | **T1556.008** |

**Description**:\
Modify CA policies to remove login restrictions (device compliance, IP restrictions).

✅ **Result**: Bypass Azure AD protections.

***

**➡️ Multi-Factor Authentication Request Generation**

\| MITRE ID | **T1111** |

**Description**:\
Flood users with fake MFA push notifications ("MFA fatigue attacks") to get accidental approval.

**Azure Example**:\
Send repeated push notifications via Azure MFA until user accepts.

✅ **Result**: MFA bypass via user exhaustion.

***

#### 🌐 Network Sniffing

\| MITRE ID | **T1040** |

**Description**:\
Capture network traffic inside Azure Virtual Networks to steal session cookies, tokens, or credentials.

**Azure Example**:\
Use packet capture on Azure VM NICs if NSG rules are misconfigured.

✅ **Result**: Harvest session tokens or cleartext credentials.

***

#### 🛡️ Steal Application Access Token

\| MITRE ID | **T1528** |

**Description**:\
Steal Azure Managed Identity tokens, Kubernetes service account tokens, or OAuth tokens from applications.

**Azure Example**:\
Steal Managed Identity token from Azure VM metadata service:

```bash
bashCopyEditcurl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"
```

✅ **Result**: Pivot into Azure services using stolen tokens.

***

#### 🔓 Unsecured Credentials

***

**➡️ Credentials In Files**

\| MITRE ID | **T1552.001** |

**Description**:\
Harvest credentials from code repositories, container images, storage blobs, or VM disks.

**Azure Example**:\
Find hardcoded secrets in Azure Blob Storage or GitHub repositories.

✅ **Result**: Immediate access to hardcoded keys.

***

**➡️ Cloud Instance Metadata API**

\| MITRE ID | **T1552.005** |

**Description**:\
Access Azure Instance Metadata Service (IMDS) to steal OAuth tokens and identity credentials.

**Azure Example**:\
Curl Azure IMDS endpoint from a compromised VM:

```bash
bashCopyEditcurl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2021-02-01"
```

✅ **Result**: Exfiltrate sensitive identity info without needing passwords.

***

## 📊 **Credential Access Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique             | MITRE ID  | Azure Example                                |
| ---------------------------------- | --------- | -------------------------------------------- |
| Password Guessing                  | T1110.001 | Guess Azure AD passwords manually            |
| Password Spraying                  | T1110.003 | Spray common passwords across accounts       |
| Credential Stuffing                | T1110.004 | Replay breached passwords                    |
| Credentials from Password Stores   | T1555.004 | Steal secrets from Azure Key Vault           |
| Web Cookies                        | T1606.003 | Steal Azure Portal session cookies           |
| SAML Tokens                        | T1606.002 | Forge Golden SAML tokens for Azure SSO       |
| Modify MFA                         | T1556.006 | Disable MFA via Conditional Access tampering |
| Modify Hybrid Identity             | T1556.007 | Abuse Azure AD Connect sync                  |
| Modify Conditional Access Policies | T1556.008 | Weaken Conditional Access policies           |
| MFA Request Generation             | T1111     | MFA fatigue attacks to exhaust users         |
| Network Sniffing                   | T1040     | Capture Azure VNET traffic                   |
| Steal Application Access Token     | T1528     | Harvest Managed Identity tokens              |
| Credentials In Files               | T1552.001 | Hardcoded secrets in storage/repos           |
| Cloud Instance Metadata API        | T1552.005 | Steal tokens from Azure VM metadata          |

***

## 🎯 Final Summary

Defending against Credential Access in Azure focuses on:

* **Hardening authentication flows (MFA, Conditional Access, Identity Protection)**
* **Securing secrets (Key Vault, Metadata Services, storage)**
* **Monitoring for brute-force and credential stuffing patterns**
* **Protecting applications and instances from token theft**
* **Detecting credential harvesting early**

##
