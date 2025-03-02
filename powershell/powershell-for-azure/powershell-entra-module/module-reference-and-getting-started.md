# Module Reference & Getting Started

## Overview:&#x20;

The following provides a list of all of the commands within the Entra PowerShell Module.&#x20;

### Login Command:

```powershell
Connect-Entra -Scopes 'User.Read.All'
```

Ensure to login with an administrator that has the proper scope. Ensure to review the permission reference in the PowerShell: Microsoft SDK section.

### List All Available Commands:

```powershell
Get-Command -Module Microsoft.Entra*
```

This returns a list of available commands

### Search for a specific command

```powershell
Get-Command -Module Microsoft.Entra* -Noun *role*
```

This returns a list of commands that match the string 'role'.

### Check Supported Properties and Methods&#x20;

```powershell
New-EntraDirectoryRoleAssignment -RoleDefinitionId 'role-id' | Get-Member
```

### Getting Command Line Help

```powershell
Get-Help Get-EntraDirectoryRoleDefinition -Detailed
```

### Documentation:

{% embed url="https://learn.microsoft.com/en-us/powershell/module/microsoft.entra/?view=entra-powershell" %}
