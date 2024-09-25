# Azure CLI

## Overview of Azure CLI&#x20;

The Azure Command-Line Interface (Azure CLI) is a powerful tool designed for managing Azure resources directly from the command line. For threat hunters who are new to Azure, understanding Azure CLI can be crucial for efficient investigation and response activities.

### **What is Azure CLI?**

Azure CLI is a cross-platform command-line tool that allows you to interact with Azure services. You can use it to perform tasks like managing resources, configuring security settings, deploying services, and gathering information that is essential for threat hunting.

**Key Features for Threat Hunters**

1. **Resource Management**: Azure CLI enables you to manage various Azure resources, such as virtual machines, storage accounts, and networking components. You can list, create, delete, and configure resources using simple commands.
2. **Security and Compliance**: You can use Azure CLI to query and manage security settings across your Azure environment. For example, you can check the status of security policies, review access controls, and ensure that resources comply with your organization’s security standards.
3. **Data Collection**: Azure CLI allows you to gather logs and metrics from various Azure services. You can use these logs to monitor unusual activities, such as unauthorized access attempts or data exfiltration, which are critical for threat detection.
4. **Automation**: You can script repetitive tasks with Azure CLI, making it easier to automate routine checks or responses to specific security incidents. This can save time and reduce the risk of human error.
5. **Interacting with Azure Security Tools**: Azure CLI can be used to interact with Azure Security Center, Azure Sentinel, and other security-focused tools. You can query alerts, investigate incidents, and even trigger automated responses directly from the command line.

### **Common Commands for Threat Hunters**

* **`az login`**: Authenticate to your Azure account. This is the first step before you can manage any resources.
* **`az group list`**: Lists all resource groups in your subscription. Resource groups are containers that hold related resources.
* **`az vm list`**: Lists all virtual machines in your environment, which can help in identifying unauthorized or suspicious instances.
* **`az monitor activity-log list`**: Retrieves activity logs, which provide insights into operations performed on resources, a vital part of threat hunting.
* **`az role assignment list`**: Shows the roles assigned to users and services, helping you identify potential privilege misuse.
* **`az storage account list`**: Lists all storage accounts, which is useful for monitoring data storage and access.

### **Practical Use Case**

Imagine you suspect that a virtual machine (VM) in your environment has been compromised. With Azure CLI, you can quickly gather details about the VM, including its network security group rules (which control inbound and outbound traffic), check who has access to it, and review the logs for any unusual activity. This streamlined approach helps you react swiftly to potential threats.

### **Getting Started**

To begin using Azure CLI, you'll need to install it on your local machine. Azure CLI is available for Windows, macOS, and Linux, and you can also use it within Azure Cloud Shell, which is an online command-line environment provided by Azure.

Once installed, you can start by logging in with `az login`, and then exploring the various commands mentioned above. The official Azure CLI documentation is also a great resource to deepen your understanding as you become more comfortable with the tool.



### **Azure CLI Documentation:**

{% embed url="https://learn.microsoft.com/en-us/cli/azure/" %}

### Azure CLI Command Reference:&#x20;

{% embed url="https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest" %}

