# Privilege Escalation TA0004

## 🛡️ **Privilege Escalation Techniques in Azure Environments**

In Microsoft Azure, adversaries use Privilege Escalation techniques to move from low-privileged users or workloads to highly privileged control over subscriptions, resource groups, or management planes. This can involve abusing Azure identity features, role manipulation, event-driven escalations, or default cloud accounts.

Escalation often blends Azure-native behavior with stealthy, automated privilege growth if defenders aren't watching.

***

#### ⬆️ Abuse Elevation Control Mechanism → **T1548**

***

**➡️ Temporary Elevated Cloud Access**

**Description**:\
Adversaries abuse Azure features like Privileged Identity Management (PIM) to request or activate Just-in-Time (JIT) privileged roles, sometimes automatically or stealthily, to escalate privileges when needed.

**Azure Example**:\
Use Azure PIM to elevate privileges for a limited time without standing permissions:

```bash
bashCopyEditaz role assignment create --assignee compromised-user --role Owner --scope /subscriptions/<sub-id>
```

_(after activating JIT assignment via PIM)_

✅ **Mapping**:\
**MITRE ID**: T1548 – _Abuse Elevation Control Mechanism_\
(Subtechnique customized for Azure JIT access, not yet separately listed in MITRE, so we map at T1548)

***

#### 👤 Account Manipulation → **T1098**

***

**➡️ T1098.001 – Additional Cloud Credentials**

**Description**:\
Adversaries add new client secrets or certificates to Azure Service Principals or Managed Identities to silently escalate access without alerting credential rotation.

**Azure Example**:

```bash
bashCopyEditaz ad sp credential reset --name <service-principal-id> --append --password <new-password>
```

✅ **Mapping**:\
**MITRE ID**: T1098.001 – _Account Manipulation: Additional Cloud Credentials_

***

**➡️ T1098.003 – Additional Cloud Roles**

**Description**:\
Assign higher Azure RBAC roles (e.g., Contributor, Owner) to compromised identities to gain elevated privileges.

**Azure Example**:

```bash
bashCopyEditaz role assignment create --assignee compromised-spn --role Owner --scope /subscriptions/<sub-id>
```

✅ **Mapping**:\
**MITRE ID**: T1098.003 – _Account Manipulation: Additional Cloud Roles_

***

**➡️ T1098.004 – SSH Authorized Keys**

**Description**:\
Modify SSH authorized keys on Azure VMs to establish privileged shell access, bypassing standard authentication.

**Azure Example**:

```bash
bashCopyEditaz vm extension set --publisher Microsoft.OSTCExtensions --name VMAccessForLinux --resource-group victim-rg --vm-name target-vm --protected-settings '{"username":"root","ssh_key":"ssh-rsa AAAAB3..."}'
```

✅ **Mapping**:\
**MITRE ID**: T1098.004 – _Account Manipulation: SSH Authorized Keys_

***

#### 📅 Event Triggered Execution → **T1546**

**Description**:\
Use Azure Event Grid, Logic Apps, or Functions to escalate privileges automatically when specific cloud events happen (e.g., when a privileged resource is created).

**Azure Example**:\
Auto-trigger a function that escalates privileges when a new VM is deployed:

```bash
bashCopyEditaz logic workflow create --resource-group victim-rg --name privilege-esc-logicapp --definition @privilegeworkflow.json
```

✅ **Mapping**:\
**MITRE ID**: T1546 – _Event Triggered Execution_

***

#### 👥 Valid Accounts → **T1078**

***

**➡️ T1078.004 – Default Accounts**

**Description**:\
Use default Azure service principals, managed identities, or platform accounts that are over-permissioned to escalate privileges silently.

**Azure Example**:\
Abuse leftover "Monitoring Agent" service principal with high privileges.

✅ **Mapping**:\
**MITRE ID**: T1078.004 – _Valid Accounts: Default Accounts_

***

**➡️ T1078.004 – Cloud Accounts**

**Description**:\
Use compromised Azure AD user or service principal accounts that have standing privileged roles (e.g., Contributor, Owner).

**Azure Example**:

```bash
bashCopyEditaz login --username privilegeduser@victimdomain.com
az role assignment list --all
```

✅ **Mapping**:\
**MITRE ID**: T1078.004 – _Valid Accounts: Cloud Accounts_

***

## 📊 **Privilege Escalation Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique            | MITRE ID      | Azure Example                                               |
| --------------------------------- | ------------- | ----------------------------------------------------------- |
| Temporary Elevated Cloud Access   | **T1548**     | Abuse Azure PIM JIT elevation                               |
| Additional Cloud Credentials      | **T1098.001** | Add client secrets to Service Principals                    |
| Additional Cloud Roles            | **T1098.003** | Assign Contributor/Owner roles                              |
| SSH Authorized Keys               | **T1098.004** | Insert privileged SSH keys into Azure VMs                   |
| Event Triggered Execution         | **T1546**     | Deploy Logic Apps or Functions triggered by events          |
| Valid Accounts → Default Accounts | **T1078.004** | Abuse leftover Azure service principals                     |
| Valid Accounts → Cloud Accounts   | **T1078.004** | Use compromised Azure AD user/service principal credentials |

***

## 🎯 Final Summary

Defending against Privilege Escalation in Azure focuses on:

* **Hardening and monitoring role assignments** (PIM, RBAC lockdown)
* **Controlling service principal and managed identity permissions**
* **Securing VMs against unauthorized SSH key insertion**
* **Restricting and auditing serverless automation (Logic Apps, Event Grid)**
* **Monitoring account behavior, login anomalies, and sudden privilege changes**

> **Privilege escalation is the pivot point. Block it = stop the blast radius.** 🛡️✅
