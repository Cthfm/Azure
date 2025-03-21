---
hidden: true
---

# Create an Azure Admin With Cloud Shell

## Overview:

The following shows you how to create an Admin User with Contributor permissions on the associated subscription

### 1. Open Cloud Shell

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

### 2. Select Powershell when the dialog box opens at the bottom of the page

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### 3. Select 'No Storage Account Required' and Select your Subscription

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

### 4. Once the Terminal is loaded, as shown below, dump the included script

```
Requesting a Cloud Shell.Succeeded. 
Connecting terminal...

Welcome to Azure Cloud Shell

Type "az" to use Azure CLI
Type "help" to learn about Cloud Shell

Your Cloud Shell session will be ephemeral so no files or system changes will persist beyond your current session.

MOTD: SqlServer has been updated to Version 22!

VERBOSE: Authenticatincle
PS /home/GA_User>
```

{% hint style="danger" %}
Ensure to replace the values with the correct domain name and use a different password please..
{% endhint %}

```powershell
# Get Subscription ID
$SubscriptionId = az account show --query "id" --output tsv

# Debug statements are GOOD
Write-Host "Using Subscription ID: $SubscriptionId"

# Ensure Subscription ID is set
if ([string]::IsNullOrEmpty($SubscriptionId)) {
    Write-Host "Error: No subscription ID found!"
    exit
}

az ad user create --display-name Azure_Admin --password password123!@# --user-principal-name Azure_Admin@<tenantname>.onmicrosoft.com

# Assign Contributor Role
az role assignment create --assignee "Azure_Admin@<tenantname>.onmicrosoft.com" `
                          --role "Contributor" `
                          --scope "/subscriptions/$SubscriptionId"
```
