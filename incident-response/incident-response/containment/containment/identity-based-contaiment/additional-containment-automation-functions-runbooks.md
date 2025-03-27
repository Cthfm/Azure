# Additional Containment - Automation Functions, Runbooks

🔍 PHASE 1: Detection of Persistence Mechanisms

#### 🔎 List Logic Apps

```bash
bashCopyEditaz logic workflow list --query "[].{Name:name, State:state, Location:location}"
```

Look for:

* Apps in **unexpected regions**
* Apps with **enabled HTTP triggers**
* Apps that **run on schedule** or react to external data

#### 🛠️ Inspect Logic App Definition (Check for Webhooks, Schedules, Secrets)

```bash
bashCopyEditaz logic workflow show --name evilApp --resource-group rg
```

> Focus on `"triggers"` and `"actions"` keys in the definition.

***

#### 🔎 List Automation Accounts & Runbooks

```bash
bashCopyEditaz automation account list --query "[].{Name:name, RG:resourceGroup}"
az automation runbook list --automation-account-name autoacct --resource-group rg
```

Check for:

* Runbooks running **as SYSTEM or Contributor**
* **Schedules** tied to weird times (e.g., 3:13 AM UTC)
* Connections to **external URLs**, PowerShell `Invoke-WebRequest`, etc.

***

#### 🔎 List Azure Functions

```bash
bashCopyEditaz functionapp list --query "[].{Name:name, State:state, Location:location}"
```

Inspect the function triggers and code:

```bash
bashCopyEditaz functionapp function show --function-name evilFunc --name funcApp --resource-group rg
```

Look for:

* `"trigger": "httpTrigger"` with open auth
* `"timerTrigger"` functions on regular intervals
* Code that references **C2 servers**, `cmd.exe`, `powershell -enc`, etc.

***

### 🔒 PHASE 2: Containment Actions

#### ❌ Disable Logic App

```bash
bashCopyEditaz logic workflow update --name evilApp --resource-group rg --state Disabled
```

#### 🔐 Remove Logic App Triggers (Kill Webhooks)

```bash
bashCopyEditaz logic workflow trigger list --resource-group rg --workflow-name evilApp
az logic workflow trigger delete --resource-group rg --workflow-name evilApp --name HttpTrigger
```

***

#### ❌ Disable Automation Runbook

```bash
bashCopyEditaz automation runbook update --automation-account-name autoacct --resource-group rg --name evilRunbook --state "Stopped"
```

#### 🚫 Remove Scheduled Jobs

```bash
bashCopyEditaz automation schedule list --automation-account-name autoacct --resource-group rg
az automation schedule delete --automation-account-name autoacct --resource-group rg --name evilSchedule
```

#### 🧼 Remove Hybrid Worker Configs (if abused)

```bash
bashCopyEditaz automation hybrid-worker-group list --automation-account-name autoacct --resource-group rg
```

***

#### ❌ Stop and Lock Down Azure Functions

```bash
bashCopyEditaz functionapp stop --name funcApp --resource-group rg
az functionapp config set --name funcApp --resource-group rg --ftps-state Disabled --http20-enabled false
```

#### 🔐 Restrict App Keys and Rotate

```bash
bashCopyEditaz functionapp keys list --name funcApp --resource-group rg
az functionapp keys set --key-name functionKey --key-value <newVal> --name funcApp --resource-group rg
```
