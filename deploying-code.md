---
hidden: true
---

# Deploying Code



## Overview:

The following is set of instructions on how to setup the code to deploy the infrastructure.&#x20;

### 1. Open A Terminal in VSCode

Use the following keyboard shortcut Ctrl+Shift+\`

{% hint style="success" %}
Normally we would use a service principal but creating a user to make this easier.&#x20;
{% endhint %}

### 2. Login with Azure Admin created in the last section

```powershell
az login 
```

### 3. Open a Terminal and  run TFState\_Build.PS1

```
CTRL+Shift+`
```

<pre><code><strong>PS C:\Users\cthfm\\code\mini_sec_l> .\tfstate_build.ps1  
</strong></code></pre>

The file will create a backend state file and ensure that you have all the Azure Service modules to complete the task.&#x20;

### 4. Initialize Terraform and run Terraform Plan

```
terraform init
terraform plan
```

This will prompt you for the region that you want to the resources to be deployed in as well as the external IP address.  This can be found here: [https://whatismyipaddress.com/](https://whatismyipaddress.com/)

### 5. Terraform Acknowledge

```
terraform apply
Enter IP and Region
<redacted summary of changes>
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

```
