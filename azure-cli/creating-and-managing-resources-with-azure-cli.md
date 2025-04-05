# Creating and Managing Resources with Azure CLI

## 5.1 Creating Virtual Machines (VMs)

Virtual Machines (VMs) are one of the **most common resources** you'll deploy in Azure.

***

#### 🛠️ Create a Linux VM

```bash
bashCopyEditaz vm create \
  --resource-group myResourceGroup \
  --name myLinuxVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

| Parameter             | Purpose                          |
| --------------------- | -------------------------------- |
| `--resource-group`    | Where the VM will be created     |
| `--name`              | Name of the VM                   |
| `--image`             | OS image (Ubuntu, Windows, etc.) |
| `--admin-username`    | Login username                   |
| `--generate-ssh-keys` | Automatically create SSH keys    |

✅ This command will create:

* VM
* Public IP
* NIC (Network Interface)
* OS Disk
* Virtual Network (if needed)

***

#### 🖥️ Create a Windows VM

```bash
bashCopyEditaz vm create \
  --resource-group myResourceGroup \
  --name myWindowsVM \
  --image Win2019Datacenter \
  --admin-username azureuser \
  --admin-password YourP@ssword123
```

**⚠️ Tip:** Passwords must meet Azure’s complexity requirements!

***

### 🔌 5.2 Connect to the VM

Get the public IP address of the VM:

```bash
bashCopyEditaz vm list-ip-addresses --name myLinuxVM --output table
```

***

#### Connect to a Linux VM:

```bash
bashCopyEditssh azureuser@<public-ip-address>
```

***

#### Connect to a Windows VM (RDP):

1. Open **Remote Desktop Connection**.
2. Enter the public IP.
3. Login with the username/password.

✅ Now you're inside your VM!

***

### 🛑 5.3 Managing a VM (Start, Stop, Restart, Delete)

| Action       | Command                                                      |
| ------------ | ------------------------------------------------------------ |
| Stop a VM    | `az vm stop --name myVM --resource-group myResourceGroup`    |
| Start a VM   | `az vm start --name myVM --resource-group myResourceGroup`   |
| Restart a VM | `az vm restart --name myVM --resource-group myResourceGroup` |
| Delete a VM  | `az vm delete --name myVM --resource-group myResourceGroup`  |

✅ **Important:** Stopping a VM **does not** delete it — it just stops billing for compute time (but storage costs remain).

***

## 📦 5.4 Creating Storage Accounts

Storage Accounts provide scalable, durable cloud storage for:

* Blobs
* Files
* Tables
* Queues

***

#### 🛠️ Create a Storage Account

```bash
bashCopyEditaz storage account create \
  --name mystorageaccount123 \
  --resource-group myResourceGroup \
  --location eastus \
  --sku Standard_LRS
```

| Parameter          | Purpose                                   |
| ------------------ | ----------------------------------------- |
| `--name`           | Globally unique name                      |
| `--resource-group` | Where the Storage Account will be created |
| `--location`       | Azure region                              |
| `--sku`            | Storage redundancy options (LRS, GRS)     |

✅ Name must be **globally unique** (only lowercase letters and numbers).

***

#### List Storage Accounts

```bash
bashCopyEditaz storage account list --output table
```

***

#### Delete a Storage Account

```bash
bashCopyEditaz storage account delete --name mystorageaccount123 --resource-group myResourceGroup
```

***

## 🌐 5.5 Creating Basic Networking Components

***

#### 🛠️ Create a Virtual Network (VNet)

```bash
bashCopyEditaz network vnet create \
  --resource-group myResourceGroup \
  --name myVNet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```

✅ This creates a VNet **and** a Subnet at the same time.

***

#### 🛡️ Create a Network Security Group (NSG)

```bash
bashCopyEditaz network nsg create \
  --resource-group myResourceGroup \
  --name myNSG
```

**NSG** controls inbound/outbound traffic to resources like VMs.

***

#### 🛡️ Create an NSG Rule to Allow SSH (Linux VM)

```bash
bashCopyEditaz network nsg rule create \
  --resource-group myResourceGroup \
  --nsg-name myNSG \
  --name allow-ssh \
  --protocol Tcp \
  --direction Inbound \
  --priority 1000 \
  --source-address-prefixes '*' \
  --source-port-ranges '*' \
  --destination-address-prefixes '*' \
  --destination-port-ranges 22 \
  --access Allow
```

✅ This opens port 22 (SSH) inbound.

***

## 🧹 5.6 Cleaning Up Resources

When you're done, delete the Resource Group to clean up everything inside it:

```bash
bashCopyEditaz group delete --name myResourceGroup
```

✅ This deletes the VMs, Storage Accounts, VNets, everything inside the group.

***

## 📝 Module 5 Summary

| Topic                        | Key Points                   |
| ---------------------------- | ---------------------------- |
| Create VMs                   | `az vm create`               |
| Connect to VMs               | SSH (Linux) or RDP (Windows) |
| Manage VMs                   | Start, stop, restart, delete |
| Create Storage Accounts      | `az storage account create`  |
| Create Networking Components | VNet, Subnet, NSG            |
| Clean up Resources           | `az group delete`            |
