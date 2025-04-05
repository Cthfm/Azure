# Installing Azure CLI

### 2.1 Installing Azure CLI

Azure CLI can be installed on **Windows**, **macOS**, or **Linux**.

| OS                    | Installation Command                |
| --------------------- | ----------------------------------- |
| Windows               | Use the MSI Installer               |
| macOS                 | `brew install azure-cli` (Homebrew) |
| Linux (Ubuntu/Debian) | Use apt-get                         |
| Linux (RHEL/Fedora)   | Use yum/dnf                         |

***

#### 🪟 Installing on Windows

1. Go to the [official download page](https://learn.microsoft.com/cli/azure/install-azure-cli).
2. Download the **MSI Installer**.
3. Run the installer (Next → Next → Finish).
4. Open **Command Prompt** or **PowerShell** and test:

```bash
bashCopyEditaz version
```

✅ You should see the installed version.

***

#### 🍎 Installing on macOS

If you use **Homebrew**:

```bash
bashCopyEditbrew update && brew install azure-cli
```

Then verify:

```bash
bashCopyEditaz version
```

***

#### 🐧 Installing on Linux (Ubuntu/Debian)

```bash
bashCopyEditcurl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Then verify:

```bash
bashCopyEditaz version
```

***

### 🔄 2.2 Updating Azure CLI

Azure CLI updates **frequently** to support new Azure services.

Update using:

| OS      | Command                                                 |
| ------- | ------------------------------------------------------- |
| Windows | Rerun the MSI installer                                 |
| macOS   | `brew upgrade azure-cli`                                |
| Linux   | `sudo apt-get update && sudo apt-get install azure-cli` |

Always try to keep your CLI updated to avoid bugs or missing features!

Check your version:

```bash
bashCopyEditaz version
```

You can view available updates using:

```bash
bashCopyEditaz upgrade
```

***

### 🔐 2.3 Logging in to Azure

After installation, you must **authenticate**.

#### Default login (interactive)

```bash
bashCopyEditaz login
```

✅ This opens a browser window asking for your Microsoft credentials.

***

#### Login with Device Code (for MFA or Cloud Shell)

If you can’t open a browser (example: SSH session):

```bash
az login --use-device-code
```

This gives you a code to enter at [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin).

***

#### Service Principal Login (for Automation)

For **automated scripts**, you should log in with a **Service Principal**:

```bash
bashCopyEditaz login --service-principal -u APP_ID -p PASSWORD --tenant TENANT_ID
```

(We'll dive into Service Principals later in the course.)

***

### 📂 2.4 Setting the Active Subscription

If you have **multiple Azure subscriptions**, you need to set the **active** one.

First, list your subscriptions:

```bash
az account list --output table
```

Example output:

| Name                 | SubscriptionId                        | State   |
| -------------------- | ------------------------------------- | ------- |
| MyCompany-Production | 1234abcd-5678-efgh-9101-ijklmnopqrst  | Enabled |
| MyCompany-Dev        | 8765zyxw-4321-vuts-1098-ponmlkjihgfed | Enabled |

***

Then set your active subscription:

```bash
az account set --subscription "MyCompany-Dev"
```

✅ Now, every command you run will operate against that subscription.

***

### 🛠️ 2.5 Verifying Your CLI Environment

Double-check everything by running:

```bash
az account show
```

You should see:

* Your current subscription
* Your tenant ID
* Your user ID

And finally:

```bash
az group list
```

If you get a valid response (even if empty), **your CLI is ready**!
