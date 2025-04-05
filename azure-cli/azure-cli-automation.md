# Azure CLI Automation

## 7.1 Why Automate Azure CLI?

Automation helps you:

| Benefit                 | Why It’s Important                           |
| ----------------------- | -------------------------------------------- |
| Save time               | Avoid manually repeating the same steps      |
| Reduce errors           | Scripts are consistent and repeatable        |
| Enable DevOps workflows | Easily integrate into CI/CD pipelines        |
| Improve scalability     | Create hundreds of resources with one script |

✅ **Scripting Azure CLI = Power and Speed.**

***

## 🛠️ 7.2 Basic Structure of an Azure CLI Script

At its core, an Azure CLI script is just **a series of CLI commands** placed in a file.

***

#### 🖥️ Example (Bash Script)

```bash
bashCopyEdit#!/bin/bash

# Variables
RESOURCE_GROUP="myScriptRG"
LOCATION="eastus"

# Create a Resource Group
az group create --name $RESOURCE_GROUP --location $LOCATION

# Create a Storage Account
az storage account create \
  --name mystorageaccount$RANDOM \
  --resource-group $RESOURCE_GROUP \
  --location $LOCATION \
  --sku Standard_LRS

# List the Storage Accounts
az storage account list --resource-group $RESOURCE_GROUP --output table
```

✅ Save this as `create_resources.sh` and run:

```bash
bashCopyEditbash create_resources.sh
```

***

#### 🖥️ Example (PowerShell Script)

```powershell
powershellCopyEdit# Variables
$ResourceGroup = "myScriptRG"
$Location = "eastus"

# Create a Resource Group
az group create --name $ResourceGroup --location $Location

# Create a Storage Account
$Random = Get-Random
az storage account create `
  --name "mystorageaccount$Random" `
  --resource-group $ResourceGroup `
  --location $Location `
  --sku Standard_LRS

# List Storage Accounts
az storage account list --resource-group $ResourceGroup --output table
```

✅ Save this as `create_resources.ps1` and run:

```powershell
powershellCopyEdit.\create_resources.ps1
```

***

## 🧩 7.3 Using Environment Variables

You can **inject dynamic values** into your scripts using environment variables.

***

#### Setting Environment Variables (Bash)

```bash
bashCopyEditexport RESOURCE_GROUP=myResourceGroup
export LOCATION=eastus
```

Then reference them in your script:

```bash
bashCopyEditaz group create --name $RESOURCE_GROUP --location $LOCATION
```

***

#### Setting Environment Variables (PowerShell)

```powershell
powershellCopyEdit$env:RESOURCE_GROUP = "myResourceGroup"
$env:LOCATION = "eastus"
```

And use:

```powershell
powershellCopyEditaz group create --name $env:RESOURCE_GROUP --location $env:LOCATION
```

✅ Using environment variables makes your scripts **portable** and **easier to maintain**.

***

## 📦 7.4 Passing Parameters into a Script

Scripts can accept input at runtime.

***

#### Bash Example with Parameters

```bash
bashCopyEdit#!/bin/bash

RESOURCE_GROUP=$1
LOCATION=$2

az group create --name $RESOURCE_GROUP --location $LOCATION
```

Run the script:

```bash
bashCopyEditbash create_rg.sh myDynamicRG eastus
```

✅ `$1`, `$2`, etc. are **positional parameters**.

***

#### PowerShell Example with Parameters

```powershell
powershellCopyEditparam(
  [string]$ResourceGroup,
  [string]$Location
)

az group create --name $ResourceGroup --location $Location
```

Run the script:

```powershell
powershellCopyEdit.\create_rg.ps1 -ResourceGroup myDynamicRG -Location eastus
```

✅ **Parameterization = More reusable scripts.**

***

## ⚡ 7.5 Best Practices for Azure CLI Automation

| Best Practice                            | Why It Matters                                  |
| ---------------------------------------- | ----------------------------------------------- |
| Use variables and parameters             | Make scripts reusable and configurable          |
| Check if resources exist before creating | Avoid duplicate deployments                     |
| Add comments to your scripts             | Make your scripts readable and maintainable     |
| Always validate input                    | Prevent unexpected errors                       |
| Handle errors gracefully                 | Use try-catch (PowerShell) or exit codes (Bash) |
| Secure sensitive data                    | Never hard-code passwords in scripts            |

***

## ✨ 7.6 Real-World Use Case Example

#### Deploy a VM Automatically

**Bash Script Example:**

```bash
bashCopyEdit#!/bin/bash

RESOURCE_GROUP="autoRG"
VM_NAME="autoVM"
LOCATION="eastus"

# Create Resource Group
az group create --name $RESOURCE_GROUP --location $LOCATION

# Deploy VM
az vm create \
  --resource-group $RESOURCE_GROUP \
  --name $VM_NAME \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys

# Output public IP
az vm list-ip-addresses --resource-group $RESOURCE_GROUP --name $VM_NAME --output table
```

✅ In just a few seconds, you’ve automated your infrastructure!

***

## 📝 Module 7 Summary

| Topic                       | Key Points                             |
| --------------------------- | -------------------------------------- |
| Why automate?               | Save time, reduce errors, scale easily |
| Structure of a script       | Series of Azure CLI commands           |
| Using environment variables | Makes scripts dynamic and maintainable |
| Passing parameters          | Makes scripts flexible                 |
| Best practices              | Secure coding, validation, reusability |
