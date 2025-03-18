---
hidden: true
---

# Deploying Code



### 1. Open A Terminal in VSCode

Use the following keyboard shortcut Ctrl+Shift+\`

### 2. Create a Service Principal to Deploy Terraform Code

<pre class="language-powershell"><code class="lang-powershell"><strong>PS C:\Users\cthfm\> az login
</strong>&#x3C;redacted>
PS C:\Users\cthfm\> az ad sp create-for-rbac --name "TerraformSP" --role="Contributor" --scopes="/subscriptions/&#x3C;subscription>"
Creating 'Contributor' role assignment under scope '/subscriptions/&#x3C;yoursubscription>'
The output includes credentials that you must protect. Be sure that you do not include these credentials in your code or check the credentials into your source control. For more information, see https://aka.ms/azadsp-cli
{
  "appId": "&#x3C;AppID>",
  "displayName": "TerraformSP",
  "password": "&#x3C;SuperSecretDontshare>",
  "tenant": "&#x3C;YourTenantID>"
}
PS C:\Users\cthfm> az logout


</code></pre>

### 3. Setup Your Environment Variables With SP Data

```powershell
$env:ARM_SUBSCRIPTION_ID="your-subscription-id"
$env:ARM_TENANT_ID="your-tenant-id"
$env:ARM_CLIENT_ID="your-client-id"
$env:ARM_CLIENT_SECRET="your-client-secret"
```

### 4. Login with the Service Principal

```powershell
az login --service-principal --username "<appId>" --password "<password>" --tenant "<tenantId>"
```



### 5. Open a Terminal and  run TFState\_Build.PS1

```
CTRL+Shift+`
```

<pre><code><strong>PS C:\Users\cthfm\\code\mini_sec_l> .\tfstate_build.ps1  
</strong></code></pre>

The file will create a backend state file and ensure that you have all the Azure Service modules to complete the task.&#x20;



### 6. Initialize Terraform and run Terraform Plan

```
terraform init
terraform plan
```

This will prompt you for the region that you want to the resources to be deployed in as well as the external IP address.  This can be found here: [https://whatismyipaddress.com/](https://whatismyipaddress.com/)



### 7. Terraform Acknowledge

```
hit yes
terraform apply
```
