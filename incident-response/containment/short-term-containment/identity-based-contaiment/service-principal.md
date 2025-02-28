# Service Principal

#### **1️⃣ Identify the Compromised Service Principal**

Before taking containment actions, identify:

* The **Service Principal ID** and associated **Application ID**.
* Its **role assignments and permissions**.
* Its **sign-in and activity logs** to detect unauthorized use.

**🔹 List All Service Principals in the Subscription:**

```azurecli
az ad sp list --query "[].{DisplayName:displayName, ObjectId:id, AppId:appId}" -o table
```

**🔹 Find Role Assignments for a Specific Service Principal:**

```azurecli
az role assignment list --assignee <service-principal-id> --query "[].{Role:roleDefinitionName, Scope:scope}" -o table
```

**🔹 Check Azure AD Sign-in Logs for the Service Principal:**

```kql
AADServicePrincipalSignInLogs
| where TimeGenerated > ago(24h)
| where AppId == "<application-id>"
| order by TimeGenerated desc
```

💡 **Signs of compromise:**

* **Unexpected sign-ins** from unusual locations/IPs.
* **Failed authentication attempts** or **token misuse**.
* **Unusual role assignments or access escalations**.

***

#### **2️⃣ Contain the Compromised Service Principal**

Once you confirm a compromise, take **immediate action** to cut off access.

**🔹 Remove Role Assignments to Restrict Access**

```azurecli
az role assignment delete --assignee <service-principal-id>
```

If multiple roles exist, remove them all:

```azurecli
az role assignment list --assignee <service-principal-id> --query "[].id" --output tsv | xargs -I {} az role assignment delete --ids {}
```

**🔹 Disable the Service Principal (Emergency Response)**

You can **disable** a service principal to immediately prevent authentication.

```azurecli
az ad sp update --id <service-principal-id> --account-enabled false
```

***

#### **3️⃣ Rotate or Remove Credentials**

Since Service Principals authenticate using **passwords** or **certificates**, you must rotate or remove them.

**🔹 List Current Credentials:**

```azurecli
azurecliCopyEditaz ad app credential list --id <application-id>
```

**🔹 Remove a Compromised Secret or Certificate:**

```azurecli
azurecliCopyEditaz ad app credential delete --id <application-id> --key-id <key-id>
```

**🔹 Add a New Secret:**

```azurecli
azurecliCopyEditaz ad app credential reset --id <application-id> --append
```

***

#### **4️⃣ Monitor for Further Threats**

After containment, **review logs** to determine the root cause and prevent future compromises.

**🔹 Query for Unauthorized API Calls by the Service Principal**

```kql
kqlCopyEditAzureDiagnostics
| where ResourceId contains "MICROSOFT.IDENTITY"
| where OperationName == "Authenticate"
| where Identity contains "<service-principal-id>"
| where ActivityStatus != "Success"
| order by TimeGenerated desc
```

**🔹 Monitor for Unusual Role Assignments**

```kql
kqlCopyEditAuditLogs
| where OperationName == "Add role assignment to service principal"
| where TargetResources contains "<service-principal-id>"
| order by TimeGenerated desc
```

***

#### **5️⃣ Reintroduce the Service Principal Securely**

If you still need the Service Principal, **reconfigure it with enhanced security**:

* **Assign least privilege roles** instead of global roles.
* **Use Managed Identities instead** where possible (since they don't rely on passwords).
* **Apply Conditional Access Policies** to restrict its usage.
* **Rotate credentials regularly** and use **Azure Key Vault** for storage.
* **Enable logging** in Microsoft Sentinel or Azure Monitor for continuous monitoring.

***

### **🛑 Final Steps**

1. **Identify the compromised service principal** and its access level.
2. **Remove or restrict its role assignments** to cut off access.
3. **Disable or rotate credentials** to prevent further abuse.
4. **Investigate logs for unauthorized access** and possible lateral movement.
5. **Reintroduce with tighter security controls**, like least privilege, managed identities, and monitorin

#### **Step 2: Revoke Access Tokens & Kill Active Sessions**

Even if you disable the SP, active tokens might still work **(especially if OAuth is abused)**.

**Revoke All Access Tokens**

Use **Microsoft Graph API** to revoke access tokens:

```http
POST https://graph.microsoft.com/v1.0/servicePrincipals/<ServicePrincipalID>/revokeSignInSessions
Authorization: Bearer <Token>
```

***

#### **Step 3: Disable the Service Principal (Temporary Lockdown)**

If you need to **immediately contain** the SP, disable it.

**Disable the SP via PowerShell**

```powershell
powershellCopyEditSet-AzureADServicePrincipal -ObjectId "<ServicePrincipalID>" -AccountEnabled $false
```

**Disable via Microsoft Graph API**

```http
PATCH https://graph.microsoft.com/v1.0/servicePrincipals/<ServicePrincipalID>
Content-Type: application/json
Authorization: Bearer <Token>

{
  "accountEnabled": false
}
```

***

#### **Step 4: Rotate or Remove Credentials**

If a **certificate or secret** has been compromised, **rotate it immediately**.

**List Current Secrets**

```powershell
Get-AzADServicePrincipal -DisplayName "<ServicePrincipalName>" | Get-AzADSpCredential
```

**Remove a Compromised Secret**

```powershell
Remove-AzADSpCredential -ObjectId "<ServicePrincipalID>" -KeyId "<CredentialKeyId>"
```

**Rotate the Secret**

1.  Generate a new **Client Secret**:

    ```powershell
    New-AzADSpCredential -ObjectId "<ServicePrincipalID>" -Password (ConvertTo-SecureString -AsPlainText "<NewSecurePassword>" -Force)
    ```
2. Update applications to use the new secret.
3. Delete the **old secret**.

**Rotate the Certificate**

1. Create a **new certificate**.
2. Add the **new certificate** to the service principal.
3. Remove the **old certificate**.

#### **Step 5: Remove Unauthorized Role Assignments**

If attackers **elevated the SP’s privileges**, revoke them.

**Check SP’s Current Role Assignments**

```powershell
Get-AzRoleAssignment -ObjectId "<ServicePrincipalID>"
```

**Remove Suspicious Role Assignments**

```powershell
Remove-AzRoleAssignment -ObjectId "<ServicePrincipalID>" -RoleDefinitionName "Owner"
```

