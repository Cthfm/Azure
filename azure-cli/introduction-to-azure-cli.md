# Introduction to Azure CLI



### What is Azure CLI?

Azure CLI (Command-Line Interface) is a cross-platform tool that allows you to create, manage, and configure Azure resources directly from your command line or terminal.

Instead of clicking around in the Azure Portal, you use simple text commands like:

```bash
az vm create --name myVM --resource-group myRG --image UbuntuLTS
```

**Key Features:**

| Feature                       | Details                                       |
| ----------------------------- | --------------------------------------------- |
| **Cross-platform**            | Runs on Windows, macOS, and Linux             |
| **Scriptable**                | Automate tasks and deployments                |
| **Consistent Experience**     | Same commands across environments             |
| **Supports JSON/YAML Output** | Useful for parsing and automation             |
| **Extendable**                | Can install additional modules ("extensions") |

***

### Why Use Azure CLI?

Here’s why people love using Azure CLI:

| Portal (GUI)                    | Azure CLI (Command Line)                     |
| ------------------------------- | -------------------------------------------- |
| Manual and click-based          | Fast, repeatable, and scriptable             |
| Harder to automate              | Easy to integrate into scripts and pipelines |
| Better for one-off simple tasks | Better for repetitive or complex tasks       |
| User-friendly for beginners     | Powerful for professionals and DevOps teams  |

You use the Portal when you want visual simplicity,\
You use the CLI when you want speed, automation, and control.

***

### How Azure CLI Fits into the Azure Ecosystem

In Azure, you can interact with your resources in four main ways:

| Method         | Description                                     | Example Tool                   |
| -------------- | ----------------------------------------------- | ------------------------------ |
| **Portal**     | Web-based user interface (click around)         | portal.azure.com               |
| **Azure CLI**  | Text-based, command-line interface              | `az vm create`                 |
| **PowerShell** | Scripting environment for system administration | `New-AzVM` (PowerShell Cmdlet) |
| **SDKs/APIs**  | Programmatic access using code                  | Python SDK, REST API           |

Azure CLI sits in the middle — perfect for engineers, sysadmins, developers, and cloud pros who need power and speed without having to write full applications.

***

### Azure CLI vs PowerShell vs Portal

| Feature        | Portal                 | Azure CLI                | Azure PowerShell                                        |
| -------------- | ---------------------- | ------------------------ | ------------------------------------------------------- |
| User Interface | Graphical              | Command-line (bash-like) | Command-line (PowerShell)                               |
| OS Support     | Browser-based          | Windows, Mac, Linux      | Primarily Windows (cross-platform with PowerShell Core) |
| Learning Curve | Easy                   | Easy to moderate         | Moderate                                                |
| Scripting      | No                     | Yes                      | Yes (more system admin tasks)                           |
| Best For       | Beginners, quick tasks | Automation, DevOps       | Deep administration and complex scripting               |

***

### Common Use Cases for Azure CLI

You’ll use Azure CLI often for tasks like:

* Deploying VMs, Storage, Databases
* Managing Resource Groups
* Setting up Networking (VNets, NSGs, Subnets)
* Automating DevOps pipelines
* Troubleshooting and monitoring
* Scripting Infrastructure as Code (IaC)

**Example:**\
Deploying a Linux VM in seconds:

```bash
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS
```
