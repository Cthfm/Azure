# Defense Evasion: TA0005

## **Defense Evasion Techniques in Entra ID (Azure Identity Environments)**

In Microsoft Entra ID (Azure AD), adversaries use Defense Evasion to **hide activities**, **bypass security controls**, **modify policies**, and **abuse trusted authentication artifacts** (tokens, credentials).

Defense evasion allows attackers to **remain stealthy**, **retain access**, and **outmaneuver detection and response**.

***

#### 🛡️ Abuse Elevation Control Mechanism → Temporary Elevated Cloud Access

\| MITRE ID | **T1548.001** |

**Description**:\
Temporarily elevate privileges through PIM (Privileged Identity Management) or Conditional Access exceptions, then remove traces by deactivating or hiding activation artifacts.

**Entra ID Example**:

* Activate Global Admin via PIM briefly, modify settings or exfiltrate data, then deactivate role.

```bash
bashCopyEditaz role assignment create --assignee compromised_user --role "Global Administrator"
# Privilege removed after use
```

✅ **Result**: Privilege appears unused after attacker finishes operations.

***

#### 🏢 Domain or Tenant Policy Modification → Trust Modification

\| MITRE ID | **T1484.002** |

**Description**:\
Modify external identity settings, B2B collaboration trusts, or federated domains to mask adversary-controlled access.

**Entra ID Example**:

* Alter B2B external collaboration policies to allow anonymous guest invites.
* Add rogue Identity Providers.

```bash
bashCopyEditaz ad external-identity create --display-name "AttackerIdP"
```

✅ **Result**: Open backdoors while blending into trusted configurations.

***

#### 💥 Impair Defenses → Disable or Modify Cloud Logs

\| MITRE ID | **T1562.008** |

**Description**:\
Disable logging (e.g., Azure AD sign-in logs, audit logs) or tamper with diagnostics settings to blind monitoring tools like Sentinel or Defender for Cloud Apps.

**Entra ID Example**:

* Modify Diagnostic Settings to stop sending logs to Log Analytics.

```bash
bashCopyEditaz monitor diagnostic-settings delete --name EntraIDLogs
```

✅ **Result**: Security operations center (SOC) loses visibility.

***

#### 🔄 Modify Authentication Process

***

**➡️ Multi-Factor Authentication (T1556.006)**

**Description**:\
Remove, reconfigure, or weaken MFA methods for accounts to bypass strong authentication requirements.

**Entra ID Example**:

* Register a new Authenticator app device or change MFA number for a compromised user.

✅ **Result**: Evasion of second-factor protections.

***

**➡️ Hybrid Identity (T1556.007)**

**Description**:\
Tamper with hybrid sync configurations (Azure AD Connect) to sync malicious on-prem users or hide rogue accounts.

**Entra ID Example**:

* Modify on-premises AD objects that sync automatically and gain cloud access without detection.

✅ **Result**: Bypass cloud-only security controls through on-prem manipulation.

***

**➡️ Conditional Access Policies (T1556.008)**

**Description**:\
Alter or disable Conditional Access (CA) policies to weaken enforcement (e.g., remove MFA requirements, exclude attacker-controlled accounts).

**Entra ID Example**:

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --state disabled
```

✅ **Result**: Evade authentication protections or restrict enforcement.

***

#### 🔑 Use Alternate Authentication Material → Application Access Token

\| MITRE ID | **T1550.001** |

**Description**:\
Steal and reuse OAuth tokens, Managed Identity tokens, or refresh tokens to impersonate users or services without needing credentials.

**Entra ID Example**:

```bash
bashCopyEditcurl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token"
```

✅ **Result**: Authenticate invisibly using stolen tokens.

***

#### 👤 Valid Accounts

***

**➡️ Default Accounts (T1078.004)**

**Description**:\
Abuse existing default or automation accounts that are overlooked or excluded from monitoring.

✅ **Result**: Hide in plain sight using under-monitored accounts.

***

**➡️ Cloud Accounts (T1078.004)**

**Description**:\
Use legitimate but compromised user accounts, avoiding abnormal login detections by mimicking normal user behavior.

✅ **Result**: Blend into everyday legitimate traffic.

***

## 📊 **Defense Evasion Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique             | MITRE ID  | Entra ID Example                                       |
| ---------------------------------- | --------- | ------------------------------------------------------ |
| Temporary Elevated Cloud Access    | T1548.001 | Abuse PIM to escalate and deactivate privilege         |
| Trust Modification                 | T1484.002 | Modify external identity trusts or federation settings |
| Disable or Modify Cloud Logs       | T1562.008 | Turn off Entra ID log diagnostics                      |
| Modify MFA                         | T1556.006 | Register or alter MFA method silently                  |
| Modify Hybrid Identity             | T1556.007 | Abuse AD Connect to sync rogue accounts                |
| Modify Conditional Access Policies | T1556.008 | Disable or weaken CA protections                       |
| Application Access Token           | T1550.001 | Use stolen OAuth tokens to authenticate                |
| Default Accounts                   | T1078.004 | Abuse unmonitored guest/SPNs                           |
| Cloud Accounts                     | T1078.004 | Hide using stolen but legitimate user accounts         |

***

## 🎯 Final Summary

Defending against Defense Evasion in Entra ID focuses on:

* **Enforcing strict control and monitoring over roles, MFA, CA policies, and trust settings**
* **Locking down token access and monitoring API usage**
* **Securing and monitoring logging infrastructure**
* **Hardening hybrid identity configurations**
