---
hidden: true
---

# Setup and Install Instructions

### Overview:

This section provides you with the instructions on what you need to install on your machine to setup the enviroment.&#x20;

### 1. Install VSCode:

Use the following link to install VSCode: [https://code.visualstudio.com/](https://code.visualstudio.com/)

### 2. Install PowerShell 7 (If it's not already installed)

```powershell
winget install --id Microsoft.Powershell --source winget
```

### 3. Ensure Script Policy Is Set to Remote Signed

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

### 4. Install AzCLI

```powershell
winget install --exact --id Microsoft.AzureCLI 
```

### 5. Install Terraform

```
winget install HashiCorp.Terraform
```

### 6. Update System's Global Path Variable

Update your system's global PATH environment variable to include the directory that contains the executable.

### 7. Verify Terraform Installed

Ensure to restart your CMD or PS session.

In a new terminal run:

```powershell
terraform -v
```

### 8. Install Git

```
winget install --id Git.Git -e --source winget
```

Ensure to restart terminal after installation&#x20;

### 9. Verify Git Installation

```
git -v
```
