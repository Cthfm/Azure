# Persistence: TA0003

## **Persistence Techniques in Entra ID (Azure Identity Environments)**

Persistence in Entra ID enables attackers to **maintain long-term access** by creating backdoor accounts, modifying roles, registering devices, altering authentication flows, or leveraging misconfigured default/cloud identities.

These techniques often occur **after initial access**, and are designed to **survive credential resets, incident response, and reboots** in cloud environments.

***

#### 👥 Account Manipulation

***

**➡️ Additional Cloud Credentials**

\| MITRE ID | **T1098.001** |

**Description**:\
Create new credentials for existing users or service principals (e.g., client secrets, certificates), enabling stealthy long-term access to Entra ID and Azure APIs.

**Entra ID Example**:

```bash
bashCopyEditaz ad sp credential reset --name <SPN-ID> --password 'NewSecret!'
```

✅ **Result**: Adversary maintains access even if original creds are revoked.

***

**➡️ Additional Cloud Roles**

\| MITRE ID | **T1098.003** |

**Description**:\
Assign new Azure roles or Entra ID directory roles to compromised accounts to escalate persistence and increase lateral access.

**Entra ID Example**:

```bash
bashCopyEditaz role assignment create --assignee <user> --role Owner
```

✅ **Result**: The attacker ensures they have persistent privilege across scopes.

***

**➡️ Device Registration**

\| MITRE ID | **T1098.004** |

**Description**:\
Register a rogue device in Entra ID to receive conditional access allowances and stay within trusted device policies.

**Entra ID Example**:

* Attacker uses a tool to register a rogue device in Entra ID as "compliant."
* Device is used to bypass CA policies requiring compliant devices.

✅ **Result**: Long-term access through a registered and “trusted” device.

***

#### ➕ Create Account → Cloud Account

\| MITRE ID | **T1136.003** |

**Description**:\
Create new Entra ID user accounts (standard or privileged) to establish persistence without using already-compromised users.

**Entra ID Example**:

```bash
bashCopyEditaz ad user create --display-name attacker --user-principal-name attacker@victimdomain.com --password 'StrongP@ss!'
```

✅ **Result**: Adversary creates a hidden backdoor account in the directory.

***

#### 🔄 Modify Authentication Process

***

**➡️ Multi-Factor Authentication (MFA)**

\| MITRE ID | **T1556.006** |

**Description**:\
Disable, modify, or register a new MFA method (e.g., Authenticator app, SMS number) on a compromised user or admin account.

**Entra ID Example**:

* Modify MFA settings via Graph API or GUI.
* Register attacker’s Authenticator device.

✅ **Result**: Persistent access via attacker-controlled MFA.

***

**➡️ Hybrid Identity**

\| MITRE ID | **T1556.007** |

**Description**:\
Abuse Entra Connect (formerly AAD Connect) sync to inject users, groups, or permissions into Entra ID from on-prem Active Directory.

**Entra ID Example**:

* Modify on-prem AD to create synced users or elevate privileges that get pushed to Entra ID.

✅ **Result**: On-prem manipulation drives persistent cloud access.

***

**➡️ Conditional Access Policies**

\| MITRE ID | **T1556.008** |

**Description**:\
Alter CA policies to weaken access controls — e.g., disable MFA, add trusted IPs, or exclude attacker-controlled accounts from key protections.

**Entra ID Example**:

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --state disabled
```

✅ **Result**: Attacker ensures uninterrupted access via policy loopholes.

***

#### 👤 Valid Accounts

***

**➡️ Default Accounts**

\| MITRE ID | **T1078.004** |

**Description**:\
Use existing guest, service principal, or automation accounts that are overprivileged or misconfigured for persistent access.

✅ **Result**: Persistence without needing to create new identities.

***

**➡️ Cloud Accounts**

\| MITRE ID | **T1078.004** |

**Description**:\
Reuse legitimate user credentials obtained via phishing, leaked creds, or token theft to maintain long-term access.

✅ **Result**: Blend in with normal user activity and evade detection.

***

## 📊 **Persistence Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique             | MITRE ID  | Entra ID Example                                        |
| ---------------------------------- | --------- | ------------------------------------------------------- |
| Additional Cloud Credentials       | T1098.001 | Add new secret/cert to service principal                |
| Additional Cloud Roles             | T1098.003 | Assign "Owner" or "Global Admin" to backdoor account    |
| Device Registration                | T1098.004 | Register attacker-controlled device to bypass CA        |
| Create Cloud Account               | T1136.003 | Create new user account in directory                    |
| Modify MFA                         | T1556.006 | Change MFA method or register attacker MFA device       |
| Modify Hybrid Identity             | T1556.007 | Use on-prem sync to create/persist users                |
| Modify Conditional Access Policies | T1556.008 | Disable or weaken CA policy for attacker                |
| Default Accounts                   | T1078.004 | Abuse misconfigured SPNs, guests, or managed identities |
| Cloud Accounts                     | T1078.004 | Reuse valid user credentials for long-term access       |

***

## 🎯 Final Summary

Defending against persistence in Entra ID focuses on:

* **Auditing account and role changes**
* **Locking down service principals and device registrations**
* **Securing and monitoring MFA configurations**
* **Hardening Conditional Access and hybrid sync pathways**

