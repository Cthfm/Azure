# Persistence: TA0003

hniques to maintain continuous access across reboots, credential rotations, and administrative clean-ups. Persistence is achieved by manipulating cloud identities, implanting malicious workloads, altering authentication processes, or leveraging trusted defaults.

***

#### 👤 Account Manipulation → **T1098 – Account Manipulation**

***

**➡️ T1098.001 – Additional Cloud Credentials**

**Description**:\
Add new authentication credentials (e.g., client secrets, certificates) to Azure Service Principals or Managed Identities to maintain access even after rotation.

**Azure Example**:

```bash
bashCopyEditaz ad sp credential reset --name <service-principal-id> --append --password <new-password>
```

✅ **Mapping**:\
**MITRE ID**: T1098.001 – _Account Manipulation: Additional Cloud Credentials_

***

**➡️ T1098.003 – Additional Cloud Roles**

**Description**:\
Assign new or elevated Azure RBAC roles to existing compromised identities to maintain privileged access.

**Azure Example**:

```bash
bashCopyEditaz role assignment create --assignee <spn-id> --role Contributor --scope /subscriptions/<sub-id>
```

✅ **Mapping**:\
**MITRE ID**: T1098.003 – _Account Manipulation: Additional Cloud Roles_

***

**➡️ T1098.004 – SSH Authorized Keys**

**Description**:\
Plant SSH keys into Azure VMs to maintain persistent remote access.

**Azure Example**:

```bash
bashCopyEditaz vm extension set --publisher Microsoft.OSTCExtensions --name VMAccessForLinux --vm-name victim-vm --resource-group victim-rg --protected-settings '{"username":"azureuser","ssh_key":"ssh-rsa AAAAB3..."}'
```

✅ **Mapping**:\
**MITRE ID**: T1098.004 – _Account Manipulation: SSH Authorized Keys_

***

#### 🛠️ Create Account → **T1136 – Create Account**

***

**➡️ T1136.003 – Cloud Account**

**Description**:\
Create hidden Azure AD users, service principals, or guest accounts for ongoing access.

**Azure Example**:

```bash
bashCopyEditaz ad sp create-for-rbac --name hidden-spn --role Reader --scopes /subscriptions/<sub-id>
```

✅ **Mapping**:\
**MITRE ID**: T1136.003 – _Create Account: Cloud Account_

***

#### 📅 Event Triggered Execution → **T1546 – Event Triggered Execution**

***

**Description**:\
Use Azure Event Grid, Logic Apps, or Functions to automatically trigger attacker-controlled operations.

**Azure Example**:

```bash
bashCopyEditaz logic workflow create --resource-group victim-rg --name evil-logicapp --definition @evilworkflow.json
```

✅ **Mapping**:\
**MITRE ID**: T1546 – _Event Triggered Execution_\
(_no subtechnique yet defined specifically for Azure Event Triggers, but still covered under general T1546_)

***

#### 🧬 Implant Internal Image → **T1587.006 – Develop Capabilities: Implant Internal Image**

***

**Description**:\
Push backdoored containers into Azure Container Registry or AKS clusters to persist access.

**Azure Example**:

```bash
bashCopyEditdocker push victimacr.azurecr.io/malicious-backdoor:latest
```

✅ **Mapping**:\
**MITRE ID**: T1587.006 – _Develop Capabilities: Implant Internal Image_

***

#### 🛡️ Modify Authentication Process → **T1556 – Modify Authentication Process**

***

**➡️ T1556.006 – Multi-Factor Authentication**

**Description**:\
Disable, weaken, or bypass MFA enforcement in Azure AD.

**Azure Example**:

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --state disabled
```

✅ **Mapping**:\
**MITRE ID**: T1556.006 – _Modify Authentication Process: Multi-Factor Authentication_

***

**➡️ T1556.007 – Hybrid Identity**

**Description**:\
Abuse Azure AD Connect to sync rogue accounts across on-premises and cloud.

**Azure Example**:

✅ **Mapping**:\
**MITRE ID**: T1556.007 – _Modify Authentication Process: Hybrid Identity_

***

**➡️ T1556.008 – Conditional Access Policies**

**Description**:\
Alter Azure Conditional Access (CA) policies to create easier access paths.

**Azure Example**:

```bash
bashCopyEditaz ad conditional-access policy update --id <policy-id> --conditions '{"locations":["trusted-location-id"]}'
```

✅ **Mapping**:\
**MITRE ID**: T1556.008 – _Modify Authentication Process: Conditional Access Policies_

***

#### 👥 Valid Accounts → **T1078 – Valid Accounts**

***

**➡️ T1078.004 – Default Accounts**

**Description**:\
Use Azure default service principals or unmanaged accounts left behind.

**Azure Example**:

✅ **Mapping**:\
**MITRE ID**: T1078.004 – _Valid Accounts: Default Accounts_

***

**➡️ T1078.004 – Cloud Accounts**

**Description**:\
Use valid stolen Azure AD user or service principal accounts for persistence.

**Azure Example**:

```bash
bashCopyEditaz login --username stolenuser@victimdomain.com
```

✅ **Mapping**:\
**MITRE ID**: T1078.004 – _Valid Accounts: Cloud Accounts_\
(_same subtechnique number, Cloud Accounts roll under Default/Cloud Service Accounts in T1078.004_)

***

## 📊 Final Mapping Table (Persistence Techniques in Azure)

| Technique/Subtechnique             | MITRE ID  | Azure Example                          |
| ---------------------------------- | --------- | -------------------------------------- |
| Additional Cloud Credentials       | T1098.001 | Add client secret to Service Principal |
| Additional Cloud Roles             | T1098.003 | Grant Contributor to SPN               |
| SSH Authorized Keys                | T1098.004 | Add SSH key via VM extension           |
| Create Cloud Account               | T1136.003 | Create hidden SPN                      |
| Event Triggered Execution          | T1546     | Deploy malicious Logic App             |
| Implant Internal Image             | T1587.006 | Push malicious container to ACR        |
| Modify MFA                         | T1556.006 | Disable CA policy enforcing MFA        |
| Modify Hybrid Identity             | T1556.007 | Abuse Azure AD Connect                 |
| Modify Conditional Access Policies | T1556.008 | Add trusted location to CA policy      |
| Default Accounts                   | T1078.004 | Use leftover SPN or managed identity   |
| Cloud Accounts                     | T1078.004 | Use stolen Azure AD user credentials   |
