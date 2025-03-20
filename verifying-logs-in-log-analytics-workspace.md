---
hidden: true
---

# Verifying Logs in Log Analytics Workspace

## Overview:

The following section goes over how to validate logs are being pushed to Azure Monitor.&#x20;

{% hint style="danger" %}
Logging can be slow in Azure and I've seen logs take up to an hour to appear.
{% endhint %}

1. Verify the logs on the list below you can search for the names as show in the snapshot

```
Event (Sysmon and AMA Windows Audit Logs created from DCR)
AzureActivityLogs - Audit Logs with Azure
AzureNetworkAnalytics_CL - Custom Table from Network Flow Logs
SignInLogs - Sign Ins for Azure
StorageBlobLogs - Storage Account Blob Logs
AzureDiagnostics - Key Vault and other resources
```

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

2. Use the following searches for each log type to confirm if logs are logging.&#x20;

```kusto
Sighin Logs

SigninLogs
| project CreatedDateTime, Identity, Location, AppDisplayName, ResultType, ResultDescription

StorageBlobLogs

StorageBlobLogs
| project TimeGenerated, AccountName, CallerIpAddress, Location, OperationName, StatusCode

Azure Activity Logs

AzureActivity
| project TimeGenerated, ResourceProviderValue, OperationNameValue, SubscriptionId, Caller, CallerIpAddress, Authorization, _ResourceId, Properties

Windows Host Based Logs
Event
| summarize count() by Source

Key Vault:

AzureDiagnostics
| where ResourceProvider contains "Microsoft.KeyVault"
| summarize count() by Category, OperationName, ResourceProvider 




```

