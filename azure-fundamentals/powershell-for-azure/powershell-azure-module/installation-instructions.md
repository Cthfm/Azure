# Installation Instructions

## Overview:

The following section goes over how to setup the Az Module within PowerShell.&#x20;

### **Installation and Setup**

1. Install the Azure PowerShell Module: The Azure PowerShell module can be installed from the PowerShell Gallery. The installation command is as follows:

```powershell
Install-Module -Name Az -AllowClobber -Scope CurrentUser
```

2. **Update the Module:** To ensure you have the latest version of the module, you can update it using:

```powershell
Update-Module -Name Az
```

3. Import the Module: Once installed, import the module into your PowerShell session:

```powershell
Import-Module Az
```

4. Sign in to Azure: Authenticate your PowerShell session with Azure using:

```powershell
Connect-AzAccount
```
