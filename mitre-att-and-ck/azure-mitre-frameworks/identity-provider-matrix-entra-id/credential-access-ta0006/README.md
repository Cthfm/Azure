# Credential Access: TA0006

## **Credential Access Techniques in Entra ID (Azure Identity Environments)**

In Microsoft Entra ID (Azure AD), adversaries use Credential Access techniques to **steal, forge, or abuse credentials** to authenticate to the cloud environment.\
Once valid credentials or tokens are stolen, attackers move easily through the identity plane.

***

#### 🔓 Brute Force

***

**➡️ Password Guessing**

\| MITRE ID | **T1110.001** |

**Description**:\
Systematically attempt common or simple passwords on Entra ID user accounts to gain access.

**Entra ID Example**:

* Target OWA, Azure Portal, or any exposed login endpoint with guessed passwords.

✅ **Result**: Simple credential breach.

***

**➡️ Password Cracking**

\| MITRE ID | **T1110.002** |

**Description**:\
Obtain password hashes from compromised databases or caches and attempt offline cracking to retrieve cleartext passwords.

**Entra ID Example**:

* Dump on-prem Active Directory password hashes and crack synced users to cloud.

✅ **Result**: Access to cloud-synced identities.

***

**➡️ Password Spraying**

\| MITRE ID | **T1110.003** |

**Description**:\
Attempt common passwords against many Entra ID accounts at once to evade account lockout policies.

**Entra ID Example**:

* Spray Office 365 login with passwords like "Spring2024!" across multiple accounts.

✅ **Result**: Broad, stealthy credential compromise.

***

**➡️ Credential Stuffing**

\| MITRE ID | **T1110.004** |

**Description**:\
Replay previously leaked username/password combinations against Entra ID services.

**Entra ID Example**:

* Use stolen credentials from a previous breach (e.g., LinkedIn, Dropbox) to login to Azure Portal.

✅ **Result**: Immediate access via credential reuse.

***

#### 💥 Exploitation for Credential Access

\| MITRE ID | **T1212** |

**Description**:\
Exploit vulnerabilities or misconfigurations to extract credentials from Azure resources or services.

**Entra ID Example**:

* Exploit misconfigured Azure Functions exposing app settings (e.g., connection strings, secrets).

✅ **Result**: Direct extraction of cloud credentials.

***

#### 🔏 Forge Web Credentials → SAML Tokens

\| MITRE ID | **T1606.002** |

**Description**:\
Steal a valid SAML signing certificate and forge SAML tokens to impersonate Entra ID users.

**Entra ID Example**:

* Perform a **Golden SAML** attack against ADFS or Azure AD Federation Services.

✅ **Result**: Persistent, stealthy access across cloud apps.

***

#### 🔄 Modify Authentication Process

***

**➡️ Multi-Factor Authentication (T1556.006)**

**Description**:\
Bypass or weaken MFA protections by manipulating user registrations or tricking users into approving fraudulent MFA prompts.

**Entra ID Example**:

* Register a rogue MFA method to a compromised user.

✅ **Result**: Bypass MFA enforcement.

***

**➡️ Hybrid Identity (T1556.007)**

**Description**:\
Compromise on-premises identities synced to Entra ID to gain cloud access without touching cloud accounts directly.

**Entra ID Example**:

* Compromise AD account → automatic access to cloud.

✅ **Result**: Hidden cloud breach through hybrid path.

***

**➡️ Conditional Access Policies (T1556.008)**

**Description**:\
Disable or modify Conditional Access policies that enforce security, allowing weak credential authentication to succeed.

**Entra ID Example**:

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --state disabled
```

✅ **Result**: Relaxed authentication paths for stolen credentials.

***

**➡️ Multi-Factor Authentication Request Generation**

\| MITRE ID | **T1111** |

**Description**:\
Trigger multiple MFA prompts (MFA bombing) to trick a user into approving an attacker’s login request.

**Entra ID Example**:

* Send dozens of push notifications to a tired or confused user.

✅ **Result**: Gain access via social engineering.

***

#### 🔑 Steal Application Access Token

\| MITRE ID | **T1528** |

**Description**:\
Steal OAuth tokens from user sessions or Managed Identities to access cloud APIs without needing passwords.

**Entra ID Example**:

```bash
bashCopyEditcurl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token"
```

✅ **Result**: Token-based authentication without passwords.

***

#### 🔏 Steal or Forge Authentication Certificates

\| MITRE ID | **T1649** |

**Description**:\
Steal certificates from Azure Key Vault, compromised admins, or misconfigured apps, then use them to forge authentication tokens.

**Entra ID Example**:

* Export authentication certificates used for SAML signing or app authentication.

✅ **Result**: Persistent credential forgery.

***

#### 🔓 Unsecured Credentials

\| MITRE ID | **T1552** |

**Description**:\
Locate credentials stored insecurely in code repositories, app settings, shared drives, or Azure resources.

**Entra ID Example**:

* Extract secrets from misconfigured Azure Storage Blobs or public GitHub repositories.

✅ **Result**: Easy credential compromise.

***

## 📊 **Credential Access Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique                     | MITRE ID  | Entra ID Example                         |
| ------------------------------------------ | --------- | ---------------------------------------- |
| Password Guessing                          | T1110.001 | Guess common passwords                   |
| Password Cracking                          | T1110.002 | Crack dumped on-prem AD hashes           |
| Password Spraying                          | T1110.003 | Spray Office 365 with seasonal passwords |
| Credential Stuffing                        | T1110.004 | Reuse leaked credentials                 |
| Exploitation for Credential Access         | T1212     | Exploit Azure Functions for secrets      |
| Forge SAML Tokens (Golden SAML)            | T1606.002 | Forge SAML assertions using stolen cert  |
| Modify MFA                                 | T1556.006 | Hijack MFA registrations                 |
| Hybrid Identity Abuse                      | T1556.007 | Attack on-prem accounts synced to cloud  |
| Modify CA Policies                         | T1556.008 | Disable CA protections                   |
| MFA Request Generation (MFA Bombing)       | T1111     | Flood MFA requests                       |
| Steal Application Access Token             | T1528     | Steal OAuth tokens                       |
| Steal or Forge Authentication Certificates | T1649     | Steal certs and forge authentication     |
| Unsecured Credentials                      | T1552     | Find secrets in Azure/GitHub             |

***

## 🎯 Final Summary

Defending against Credential Access in Entra ID focuses on:

* **Enforcing strong, phishing-resistant MFA everywhere**
* **Hardening and auditing token-based authentication paths**
* **Securing secrets and authentication materials**
* **Detecting brute force, credential stuffing, and stolen credential reuse early**
