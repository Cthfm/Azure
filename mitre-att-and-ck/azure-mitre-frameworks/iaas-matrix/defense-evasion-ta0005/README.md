# Defense Evasion TA0005

* **Hardening and monitoring identity, authentication, and access flows**
* **Protecting security configurations from unauthorized modification**
* **Watching for attacker-triggered changes in compute, network, and logging**
* **Detecting the use of stolen tokens, cookies, and rogue accounts**

Defending against Defense Evasion in Azure focuses on:

## 🎯 Final Summary

***

| Technique/Subtechnique              | MITRE ID  | Azure Example                                |
| ----------------------------------- | --------- | -------------------------------------------- |
| Temporary Elevated Cloud Access     | T1548     | JIT PIM elevation to disable controls        |
| Exploitation for Defense Evasion    | T1211     | Exploit misconfigs to bypass defenses        |
| Disable or Modify Tools             | T1562.001 | Disable Defender for Cloud settings          |
| Disable or Modify Cloud Firewall    | T1562.007 | Delete or weaken NSG rules, WAF              |
| Disable or Modify Cloud Logs        | T1562.008 | Remove Azure Diagnostic Settings             |
| Modify MFA                          | T1556.006 | Disable Conditional Access enforcing MFA     |
| Modify Hybrid Identity              | T1556.007 | Tamper with Azure AD Connect                 |
| Modify Conditional Access Policies  | T1556.008 | Weaken or exclude CA protections             |
| Create Snapshot                     | T1578.002 | Snapshot VMs silently                        |
| Create Cloud Instance               | T1578.001 | Deploy hidden cloned VMs                     |
| Delete Cloud Instance               | T1578.003 | Destroy forensic evidence                    |
| Revert Cloud Instance               | T1578.004 | Revert VMs to clean snapshots                |
| Modify Cloud Compute Configurations | T1578.005 | Remove monitoring, alter settings            |
| Modify Cloud Resource Hierarchy     | T1578     | Alter Azure Management Groups/subscriptions  |
| Unused/Unsupported Cloud Regions    | T1578     | Deploy to lesser-monitored regions           |
| Application Access Token            | T1550.001 | Steal and reuse managed identity tokens      |
| Web Session Cookie                  | T1550.004 | Steal and reuse Azure Portal session cookies |
| Default Accounts                    | T1078.004 | Abuse Azure defaults (SPNs, identities)      |
| Cloud Accounts                      | T1078.004 | Use stolen Azure AD identities               |

## 📊 **Defense Evasion Techniques in Azure (MITRE Mapped)**

***

✅ **Result**: Normal-looking access paths.

**Description**:\
Use compromised Azure AD user or service principal accounts for operations without raising suspicion.

\| MITRE ID | **T1078.004** |

**➡️ Cloud Accounts**

***

✅ **Result**: Blend into legitimate account usage.

**Description**:\
Use Azure default service principals or managed identities to hide activities under legitimate accounts.

\| MITRE ID | **T1078.004** |

**➡️ Default Accounts**

***

#### 👥 Valid Accounts

***

✅ **Result**: No need to reauthenticate visibly.

**Description**:\
Steal and replay Azure Portal web session cookies for console access.

\| MITRE ID | **T1550.004** |

**➡️ Web Session Cookie**

***

✅ **Result**: Pivot stealthily using existing session tokens.

```bash
bashCopyEditcat /var/run/secrets/kubernetes.io/serviceaccount/token
```

**Azure Example**:

**Description**:\
Steal and reuse Azure service principal tokens or managed identity tokens to access resources without normal authentication.

\| MITRE ID | **T1550.001** |

**➡️ Application Access Token**

***

#### 🛡️ Use Alternate Authentication Material

***

✅ **Result**: Attack operations hidden geographically.

**Description**:\
Deploy resources into less-monitored Azure regions to avoid centralized detection (e.g., regions not covered by SIEM, Defender).

\| MITRE ID | **T1578** (_customized Azure usage_) |

#### 🌎 Unused/Unsupported Cloud Regions

***

✅ **Result**: Attackers hide activities under altered structures.

**Description**:\
Modify Azure Management Groups, Subscriptions, or Resource Group hierarchies to create hidden or isolated environments for attacker operations.

\| MITRE ID | **T1578** |

#### 🏢 Modify Cloud Resource Hierarchy

***

✅ **Result**: Remove defender visibility inside VMs.

**Description**:\
Modify VM extensions, networking, storage, or OS configurations to remove monitoring agents or restrict logging.

\| MITRE ID | **T1578.005** |

**➡️ Modify Cloud Compute Configurations**

***

✅ **Result**: Attack footprints wiped clean.

**Description**:\
Revert a VM to a previously known clean snapshot to erase traces of attacker activities.

\| MITRE ID | **T1578.004** |

**➡️ Revert Cloud Instance**

***

✅ **Result**: Erases forensic evidence.

```bash
bashCopyEditaz vm delete --resource-group victim-rg --name evidence-vm --yes
```

**Azure Example**:

**Description**:\
Delete VMs to destroy evidence or prevent forensic recovery.

\| MITRE ID | **T1578.003** |

**➡️ Delete Cloud Instance**

***

✅ **Result**: Hidden cloned VMs deployed.

```bash
bashCopyEditaz vm create --resource-group victim-rg --name cloned-vm --attach-os-disk stealth-snapshot
```

**Azure Example**:

**Description**:\
Clone or deploy new VMs from existing snapshots for persistence or staging C2.

\| MITRE ID | **T1578.001** |

**➡️ Create Cloud Instance**

***

✅ **Result**: Steal OS disks stealthily.

```bash
bashCopyEditaz snapshot create --resource-group victim-rg --source victim-vm --name stealth-snapshot
```

**Azure Example**:

**Description**:\
Create snapshots of Azure VMs to steal data or credentials without alerting on live systems.

\| MITRE ID | **T1578.002** |

**➡️ Create Snapshot**

***

#### 🖥️ Modify Cloud Compute Infrastructure

***

✅ **Result**: Easier reentry paths for attackers.

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --conditions '{"locations":["trusted-location-id"]}'
```

**Azure Example**:

**Description**:\
Modify Conditional Access (CA) policies to allow risky access locations, IPs, devices, or users.

\| MITRE ID | **T1556.008** |

**➡️ Conditional Access Policies**

***

✅ **Result**: Persist across both environments stealthily.

**Description**:\
Manipulate Azure AD Connect or hybrid synchronization settings to evade detection through on-premise-to-cloud identity links.

\| MITRE ID | **T1556.007** |

**➡️ Hybrid Identity**

***

✅ **Result**: MFA protection removed or bypassed.

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --state disabled
```

**Azure Example**:

**Description**:\
Tamper with or disable Azure Conditional Access policies enforcing MFA.

\| MITRE ID | **T1556.006** |

**➡️ Multi-Factor Authentication**

***

#### 🛡️ Modify Authentication Process

***

✅ **Result**: Logging pipelines are broken, delaying detection.

```bash
bashCopyEditaz monitor diagnostic-settings delete --name "diag-settings" --resource <resource-id>
```

**Azure Example**:

**Description**:\
Disable, delete, or modify Azure Activity Logs, Diagnostic Settings, or Log Analytics configurations to blind defenders.

\| MITRE ID | **T1562.008** |

**➡️ Disable or Modify Cloud Logs**

***

✅ **Result**: Traffic control barriers removed.

```bash
bashCopyEditaz network nsg rule delete --resource-group victim-rg --nsg-name victim-nsg --name AllowSSHInbound
```

**Azure Example**:

**Description**:\
Disable or modify Azure-native firewall protections such as Azure Firewall, NSGs, or Application Gateway WAFs to allow unrestricted lateral movement or C2 channels.

\| MITRE ID | **T1562.007** |

**➡️ Disable or Modify Cloud Firewall**

***

✅ **Result**: Monitoring agents or cloud-native security solutions are disabled.

```bash
bashCopyEditaz security setting update --name MCAS --setting-state Disabled
```

**Azure Example**:

**Description**:\
Disable or tamper with security monitoring tools like Microsoft Defender for Cloud, Azure Monitor agents, or threat protection settings.

\| MITRE ID | **T1562.001** |

**➡️ Disable or Modify Tools**

***

#### 🛡️ Impair Defenses

***

✅ **Result**: Security controls bypassed via misconfiguration exploitation.

Exploit a misconfigured Azure Function or Logic App that allows privilege modification without audit logging enabled.

**Azure Example**:

**Description**:\
Exploit misconfigurations or vulnerabilities in Azure services or workloads specifically to bypass defenses (e.g., disable Defender plans, misconfigure NSGs or Diagnostic Settings).

\| MITRE ID | **T1211** |

#### 🎭 Exploitation for Defense Evasion

***

✅ **Result**: Short-lived elevation helps evade long-term detection.

```bash
bashCopyEditaz role assignment create --assignee compromised-user --role Owner --scope /subscriptions/<sub-id>
```

**Azure Example**:

**Description**:\
Abuse Azure Privileged Identity Management (PIM) to temporarily elevate privileges to modify security settings, audit logs, or create backdoors without persistent standing privilege.

| MITRE ID | **T1548** |
| -------- | --------- |

#### 🎭 Abuse Elevation Control Mechanism → Temporary Elevated Cloud Access

***

In Microsoft Azure, adversaries use Defense Evasion techniques to avoid detection, disable security tooling, modify authentication controls, and blend into legitimate cloud operations. Defense Evasion allows attackers to **persist longer**, **escalate stealthily**, and **prepare for impact or exfiltration**.

## **Defense Evasion Techniques in Azure Environments**

## ltrate sensitive data:

* ```
  az snapshot create --resource-group MyResourceGroup --source MyOSDisk --name MySnapshot
  ```

**Create Cloud Instance (T1578.002)**

* **Example:** An attacker creates a new Azure VM in a different region to establish persistence and avoid detection.

**Delete Cloud Instance (T1578.003)**

*   **Example:** After exfiltrating data, an attacker deletes audit-related VM instances:

    ```powershell
    az vm delete --resource-group MyResourceGroup --name AuditVM --yes
    ```

**Revert Cloud Instance (T1578.004)**

* **Example:** An attacker restores an Azure VM from an older snapshot to erase security patches.

**Modify Cloud Compute Configurations (T1578.005)**

* **Example:** An attacker alters an Azure VM’s diagnostic settings to stop security monitoring.

#### **Modify Cloud Resource Hierarchy (**&#x54;1666)

Attackers manipulate cloud structures to avoid detection and maintain persistence.&#x20;

* **Example:** An attacker with elevated privileges may create new subscriptions and deploy new resources. They can move subscriptions from a victim tenant to an attacker-controlled tenant.

#### **Unused/Unsupported Cloud Regions (T1535)**

Attackers use regions that are not actively monitored or utilized within an environment to evade detection.

* **Example:** An attacker deploys resources in an Azure region not actively monitored by security teams to evade detection.

#### **Use Alternate Authentication Material (T1550)**

Attackers bypass traditional authentication mechanisms and avoid detection. Instead of using stolen passwords, adversaries leverage authentication mechanisms to authenticate without triggering login failure alerts or multi-factor authentication (MFA) challenges.

**Application Access Token (T1550.001)**

* **Example:** An attacker extracts an Azure Entra OAuth token from a compromised user's machine and uses it to authenticate API requests.

**Web Session Cookie (T1550.004)**

* **Example:** An attacker steals an authenticated Azure session cookie using a myriad of ways such as a "pass-the-cookie" attack.

#### **Valid Accounts (T1078)**

Attackers leverage legitimate credentials to blend in with normal user activity, avoiding detection. Instead of exploiting vulnerabilities, they use stolen, default, or misconfigured accounts to access systems without triggering security alerts. This includes compromised user accounts, service accounts, cloud credentials, or SSH keys, allowing attackers to persist within networks while bypassing traditional security mechanisms like failed login alerts or brute-force protections.

**Default Accounts (T1078.001)**

* **Example:** An attacker exploits an Azure Storage Account configured with a default shared access key to access stored files.

**Cloud Accounts (T1078.004)**

* **Example:** An attacker uses leaked Azure admin credentials from GitHub to log into the Azure portal and modify security configurations.
