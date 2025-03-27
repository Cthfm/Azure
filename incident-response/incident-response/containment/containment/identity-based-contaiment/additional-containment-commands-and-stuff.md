# Additional Containment - Commands and Stuff

### 🧨 PHASE 2 — Containment Actions

#### 🧑‍💻 Identity Containment

| Action                 | Command                                                                                 |
| ---------------------- | --------------------------------------------------------------------------------------- |
| Disable AAD User       | `az ad user update --id user@domain.com --account-enabled false`                        |
| Revoke Tokens          | `az ad sign-in revoke --user-id user@domain.com`                                        |
| Remove Role Assignment | `az role assignment delete --assignee user@domain.com --role Owner`                     |
| Reset Password         | `Set-AzureADUserPassword -ObjectId user@domain.com -ForceChangePasswordNextLogin $true` |
| Kill MFA Sessions      | Use MS Graph API to revoke `RefreshTokens`                                              |
| Revoke Guest Access    | `az ad user delete --id guest@domain.com`                                               |

***

#### ☁️ Compute Containment

| Action                    | Command                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------ |
| Stop VM                   | `az vm deallocate --name vm --resource-group rg`                                           |
| Isolate VM                | `az network nic update --name nic --resource-group rg --remove ipConfigurations 0`         |
| Move to Quarantine Subnet | Update NIC to new isolated subnet                                                          |
| Snapshot Disk             | `az snapshot create --resource-group rg --name snap --source /subscriptions/...`           |
| Reset Admin Password      | `az vm user update --name vm --resource-group rg --username admin --password NewP@ssw0rd!` |

***

#### 📦 Storage Containment

| Action                   | Command                                                                 |
| ------------------------ | ----------------------------------------------------------------------- |
| Regenerate Keys          | `az storage account keys renew --account-name stg --key primary`        |
| Disable Public Access    | `az storage account update --name stg --allow-blob-public-access false` |
| Revoke Access SAS Tokens | Rotate keys to invalidate tokens                                        |
| Enable Logging           | Azure Monitor Logs                                                      |

***

#### 🏗️ Network Containment

| Action                       | Command                                               |
| ---------------------------- | ----------------------------------------------------- |
| Block C2 Outbound IPs        | Create NSG rule (deny outbound)                       |
| Quarantine Subnet/VNET       | `az network vnet subnet create --name quarantine ...` |
| Remove Public IPs            | `az network public-ip delete`                         |
| Apply Just-In-Time VM Access | Defender for Cloud blade                              |
| Enable NSG Flow Logs         | Diagnostic Settings > NSG                             |

***

#### 🔐 Secrets & Key Vault Containment

| Action                              | Command                                                                  |
| ----------------------------------- | ------------------------------------------------------------------------ |
| Rotate Secrets                      | `az keyvault secret set --vault-name vault --name secret --value newval` |
| Purge Secrets                       | `az keyvault secret purge --vault-name vault --name secret`              |
| Rotate Certs & Keys                 | KeyVault portal or CLI                                                   |
| Enable RBAC / Disable public access | `az keyvault update --enable-rbac-authorization true`                    |

***

#### 🤖 Service Principals & Automation

| Action                          | Command                                                                        |
| ------------------------------- | ------------------------------------------------------------------------------ |
| List All SPNs with Roles        | `az role assignment list --all --query "[?principalType=='ServicePrincipal']"` |
| Delete Malicious SPN            | `az ad sp delete --id appId`                                                   |
| Rotate SPN Credentials          | CLI or Portal                                                                  |
| Kill Automation Account Scripts | `az automation account delete`                                                 |
| Kill Logic Apps & Functions     | `az logic workflow delete`, `az functionapp delete`                            |

***

#### 🎯 Privilege Management

| Action                         | Command                                 |
| ------------------------------ | --------------------------------------- |
| Audit Role Assignments         | `az role assignment list --all --query` |
| Disable PIM Users Temporarily  | AzureAD / Graph API                     |
| Restrict Elevated Roles to PIM | RBAC Policy / PIM Enforcement           |
| Audit Azure Lighthouse Access  | `az managedservices assignment list`    |



### ✅ Summary Table: Containment for Azure Lighthouse

| Action              | Command or Method                      |
| ------------------- | -------------------------------------- |
| 🔍 List Delegations | `az managedservices assignment list`   |
| ❌ Delete Delegation | `az managedservices assignment delete` |
