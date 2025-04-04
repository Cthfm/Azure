# Initial Access: TA0001

## **Initial Access Techniques in Entra ID (Azure Identity Environments)**

In Microsoft Entra ID (Azure Active Directory), adversaries use Initial Access techniques to gain a **foothold into the cloud identity plane**.\
This includes phishing users, abusing trusted federations (B2B collaboration, cross-tenant access), or exploiting weak/default cloud identities.

Identity is the **entry point** for most cloud breaches — protecting Entra ID is your first line of defense.

***

#### 🎯 Drive-by Compromise

\| MITRE ID | **T1189** |

**Description**:\
An adversary compromises a user’s device by tricking them into visiting a malicious website that silently exploits vulnerabilities or drops malware (e.g., token stealers, session hijackers).

**Entra ID Example**:

* Victim visits a malicious site that injects a rogue OAuth application consent prompt ("Consent phishing").
* The user unknowingly grants the malicious app access to their Microsoft 365 or Azure resources.

```bash
bashCopyEdit# Rogue app request
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=<malicious-app-id>&response_type=code&scope=openid+profile+user.read+mail.read
```

✅ **Result**: Adversary gains OAuth token access to Entra ID-protected resources without needing credentials.

***

#### 🎣 Phishing

***

**➡️ Spearphishing Link**

\| MITRE ID | **T1566.002** |

**Description**:\
Send a targeted email containing a malicious link that steals Entra ID credentials, MFA codes, or session cookies when clicked.

**Entra ID Example**:

* Victim receives a phishing email mimicking Microsoft login.
* Link redirects to an Azure-like phishing page (`login.microsoftonline.com.fake.site`) capturing credentials.

✅ **Result**: Adversary harvests credentials and possibly MFA tokens, gaining Entra ID access.

***

**➡️ Spearphishing Voice (Vishing)**

\| MITRE ID | **T1566.004** |

**Description**:\
Call targeted users pretending to be Microsoft support or IT helpdesk and trick them into revealing credentials, MFA codes, or approving MFA push notifications.

**Entra ID Example**:

* Victim receives a call instructing them to "verify" their MFA code or approve an MFA prompt.
* Attacker simultaneously attempts login and tricks victim into approving.

✅ **Result**: Adversary bypasses MFA and gains account access.

***

#### 🔗 Trusted Relationship

\| MITRE ID | **T1199** |

**Description**:\
Abuse federated identities, cross-tenant B2B access, or delegated admin privileges to gain access to Entra ID resources.

**Entra ID Example**:

* Attacker compromises an account from a trusted external tenant (Azure B2B collaboration).
* Uses trust relationship to access internal Entra ID groups, apps, or resources.

```bash
bashCopyEdit# External user login
az login --username compromised_user@trustedtenant.com
az ad user list
```

✅ **Result**: Access internal resources without needing direct exploitation.

***

#### 👤 Valid Accounts

***

**➡️ Default Accounts**

\| MITRE ID | **T1078.004** |

**Description**:\
Abuse default service principals, automation accounts, managed identities, or misconfigured guest accounts in Entra ID.

**Entra ID Example**:

* An attacker finds a default Entra ID guest account that still has "Contributor" role assigned in Azure subscriptions.

✅ **Result**: Immediate access using poorly configured identities.

***

**➡️ Cloud Accounts**

\| MITRE ID | **T1078.004** |

**Description**:\
Use stolen or leaked Entra ID cloud user accounts (standard users, admins, service principals) to authenticate directly.

**Entra ID Example**:

* Attacker phishes a standard Entra ID user or recovers leaked Office 365 credentials.
* Logs into Azure and enumerates environment.

```bash
bashCopyEditaz login --username phisheduser@victimdomain.com
```

✅ **Result**: Legitimate-looking session inside Entra ID and Azure.

***

## 📊 **Initial Access Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique        | MITRE ID  | Entra ID Example                                       |
| ----------------------------- | --------- | ------------------------------------------------------ |
| Drive-by Compromise           | T1189     | OAuth app consent phishing via rogue site              |
| Spearphishing Link            | T1566.002 | Email phishing with Azure login clone                  |
| Spearphishing Voice (Vishing) | T1566.004 | Fake IT support call to capture MFA code               |
| Trusted Relationship          | T1199     | Abuse external Azure AD B2B tenant trust               |
| Default Accounts              | T1078.004 | Misconfigured guest/service principal usage            |
| Cloud Accounts                | T1078.004 | Use stolen cloud user or service principal credentials |

***

## 🎯 Final Summary

Defending against Initial Access in Entra ID focuses on:

* **Hardening user authentication flows (MFA, CA policies, phishing-resistant auth)**
* **Securing and monitoring trusted relationships**
* **Reducing the blast radius of default, guest, and service principal accounts**
* **Detecting credential phishing attempts early**

###
