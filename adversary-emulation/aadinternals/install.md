# Install

## **Installation and Usage**

The following provides instructions for install and simple commands for usage.

{% hint style="info" %}
**Pre-requisites**: PowerShell 7.x or later.
{% endhint %}

### **Installation Instructions**

```powershell
Install-Module AADInternals
Import-Module AADInternals
```

### **Example Commands**&#x20;

&#x20;**Retrieving Tenant details**

```powershell
Get-AADIntTenantDetails
```

**Generate a Password Spray Attack**:

```powershell
Invoke-AADIntPasswordSpray -UserList users.txt -Password Summer2024
```
