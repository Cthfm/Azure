---
hidden: true
---

# Verifying Logs in Log Analytics Workspace

## Overview:

The following section goes over how to validate logs are being pushed to Azure Monitor.&#x20;

{% hint style="danger" %}
I have noticed delays in logging to start in the LAW with VNET and NSG related logs. It may take a while, a few hours, in order for this to start logging.&#x20;
{% endhint %}

### 1. Verify the logs on the list below you can search for the names as show in the snapshot.

```
Event (Sysmon and AMA Windows Audit Logs created from DCR)
AzureActivityLogs - Audit Logs with Azure
AzureNetworkAnalytics_CL - Custom Table from NSG Flow Logs
AzureNetworkAnalyticsIPDetails_CL - Custom Table with IP Insights for NSGs
SignInLogs - Sign Ins for Azure
StorageBlobLogs - Storage Account Blob Logs
AzureDiagnostics - Key Vault and other resources
Perf - AMA Performance Logs for VM
NTANetAnalytics - VNET Flow Logs
NTAIpDetails - IP Details from VNet Flow Logs
DNSQueryLogs - DNS Query Logs
```

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### 2. Use the following searches for each log type to confirm if logs are logging.&#x20;

{% hint style="warning" %}
If the tables are not populating it is most likely due to logs not being generated.
{% endhint %}

```kusto
Sigin Logs

SigninLogs
| project CreatedDateTime, Identity, Location, AppDisplayName, ResultType, ResultDescription

StorageBlobLogs

StorageBlobLogs
| project TimeGenerated, AccountName, CallerIpAddress, Location, OperationName, StatusCode

Azure Activity Logs

AzureActivity
| project TimeGenerated, ResourceProviderValue, OperationNameValue, SubscriptionId, Caller, CallerIpAddress, Authorization, _ResourceId, Properties

Windows Host Based Activity Logs
Event
| summarize count() by Source

Key Vault:

AzureDiagnostics
| where ResourceProvider contains "Microsoft.KeyVault"
| summarize count() by Category, OperationName, ResourceProvider 

VM Performance Monitoring

Perf
| project TimeGenerated, Computer, ObjectName, CounterName, InstanceName, CounterValue, CounterPath, _ResourceId

NTAIpDetails (IP Details from Flow Logs)

NTAIpDetails
| project TimeGenerated, FlowType, Ip, PublicIpDetails, ThreatType, ThreatDescription, Location

VNET Netflow Logs

NTANetAnalytics
| project TimeGenerated, FlowType, FlowDirection, FlowStatus, FlowStartTime, FlowEndTime, SrcIp, SrcPublicIps, DestIp,DestPublicIps, DestPort, L4Protocol, L7Protocol

DNS Query Logs:

DNSQueryLogs
| project TimeGenerated, Region, VirtualNetworkId, QueryType, QueryClass, QueryName, Answer, OperationName

```

