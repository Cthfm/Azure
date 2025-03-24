---
hidden: true
---

# Create an Azure Admin With Cloud Shell

## Overview:

The following shows you how to create an Admin User with Contributor permissions on the associated subscription. In order to not use the GA account for activities and use a lesser privilege role we create this 'Azure Admin' role.&#x20;

### 1. Open Cloud Shell

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 2. Select Powershell when the dialog box opens at the bottom of the page

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### 3. Select 'No Storage Account Required', Select your Subscription, and click apply.

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

# Output the subscription ID to user to show what is being set. 
Write-Host "Using Subscription ID: $SubscriptionId"

# Verify that the subscription was set.
if ([string]::IsNullOrEmpty($SubscriptionId)) {
    Write-Host "Error: No subscription ID found!"
    exit
}

az ad user create --display-name Azure_Admin2 --password password123!@ --user-principal-name Azure_Admin2@cthfm.onmicrosoft.com

# Assign Contributor Role
az role assignment create --assignee "Azure_Admin2@cthfm.onmicrosoft.com" `
                          --role "Contributor" `
                          --scope "/subscriptions/$SubscriptionId"
```
