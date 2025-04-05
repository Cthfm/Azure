# Resource Group Management

### 4.1 What is a Resource Group?

A **Resource Group** in Azure is a **container** that holds related resources for an Azure solution.

**Examples of resources:**

* Virtual Machines (VMs)
* Storage Accounts
* Databases
* Virtual Networks (VNets)

***

| Key Characteristics   | Why It Matters                                                 |
| --------------------- | -------------------------------------------------------------- |
| Logical grouping      | Organize your environment                                      |
| Simplified management | Apply permissions, policies, and monitoring at the group level |
| Billing               | View costs by resource group                                   |
| Lifecycle management  | Delete all resources together when no longer needed            |

✅ **Think of a Resource Group as a folder for your Azure stuff.**

***

### 🛠️ 4.2 Creating a Resource Group

Basic command structure:

```bash
bashCopyEditaz group create --name <resource-group-name> --location <location>
```

#### 🛠️ Example:

```bash
bashCopyEditaz group create --name myTestRG --location eastus
```

* `--name`: Name of your resource group
* `--location`: Azure region where metadata is stored

✅ Successful output will show the new Resource Group details in JSON.

***

#### ⚡ Quick Tip:

The **location** for a Resource Group does **not** limit where your resources can be deployed — it only stores **metadata** about the group itself.

***

### 📋 4.3 Listing Resource Groups

View all Resource Groups in your subscription:

```bash
bashCopyEditaz group list --output table
```

| Name      | Location | Status    |
| --------- | -------- | --------- |
| myTestRG  | eastus   | Succeeded |
| prodGroup | westus2  | Succeeded |

✅ **Best Practice:** Use `--output table` for a nice readable format.

***

#### Filtering with `--query`

List just the names of your Resource Groups:

```bash
bashCopyEditaz group list --query "[].name" --output table
```

Result:

| Name      |
| --------- |
| myTestRG  |
| prodGroup |

***

### 🔎 4.4 Viewing a Specific Resource Group

You can get detailed information about a specific Resource Group:

```bash
bashCopyEditaz group show --name <resource-group-name>
```

#### 🛠️ Example:

```bash
bashCopyEditaz group show --name myTestRG --output yaml
```

✅ Output will show properties like:

* Location
* Tags
* Resource Group ID
* Provisioning State

***

### 🗑️ 4.5 Deleting a Resource Group

Deleting a Resource Group **deletes everything inside it** — use carefully!

Command:

```bash
bashCopyEditaz group delete --name <resource-group-name>
```

You’ll usually be prompted for confirmation.

#### 🛠️ Example:

```bash
bashCopyEditaz group delete --name myTestRG
```

#### Force delete without confirmation:

```bash
bashCopyEditaz group delete --name myTestRG --yes --no-wait
```

* `--yes`: Skip confirmation
* `--no-wait`: Return immediately instead of waiting for the delete operation to complete

***

### 💡 4.6 Best Practices for Managing Resource Groups

| Best Practice                | Why It Matters                                             |
| ---------------------------- | ---------------------------------------------------------- |
| Group resources by lifecycle | E.g., group dev resources separately from prod             |
| Use naming conventions       | Makes it easy to search and automate (e.g., `rg-prod-web`) |
| Apply tags                   | Add metadata like project name, environment, owner         |
| Clean up unused groups       | Saves costs and reduces clutter                            |

***

## 📝 Module 4 Summary

| Topic                     | Key Points                                            |
| ------------------------- | ----------------------------------------------------- |
| What is a Resource Group? | A logical container for Azure resources               |
| Create a group            | `az group create --name <name> --location <location>` |
| List groups               | `az group list --output table`                        |
| View a group's details    | `az group show --name <name>`                         |
| Delete a group            | `az group delete --name <name>`                       |
| Best practices            | Naming, tagging, grouping by lifecycle, cleanup       |
