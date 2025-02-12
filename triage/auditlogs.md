---
hidden: true
---

# AuditLogs

## Overview:

The following are some basic KQL commands to do principal-based triage. This table is for Entra ID. It Includes system activity information about user and group management managed applications and directory activities.

{% hint style="danger" %}
These are merely ideas and can be developed to meet your organization needs.
{% endhint %}

### 1. Overview Search

This search will show the overview of the user or app activities with key fields.

```kusto
AuditLogs|
extend initiatedByJson = parse_json(InitiatedBy)  // Parse InitiatedBy JSON
| extend user_id = tostring(initiatedByJson.user.id),
         user_displayName = tostring(initiatedByJson.user.displayName),
         user_principalName = tostring(initiatedByJson.user.userPrincipalName),
         app_id = tostring(initiatedByJson.app.id),
         app_displayName = tostring(initiatedByJson.app.displayName)
| where user_principalName == "badactor@cthfm.com"  // Filter on user
| project user_principalName, ActivityDisplayName, Resource, ResourceGroup, AdditionalDetails, TargetResources, LoggedByService, Result
```

### 2. Services and Operations Completed by Application or User

This shows the services that the user or application interacted with and the associated count. This gives us the scope of the activity within a given time frame.

<pre class="language-kusto"><code class="lang-kusto"><strong>AuditLogs
</strong>|extend initiatedByJson = parse_json(InitiatedBy)  // Parse InitiatedBy JSON
| extend user_id = tostring(initiatedByJson.user.id),
         user_displayName = tostring(initiatedByJson.user.displayName),
         user_principalName = tostring(initiatedByJson.user.userPrincipalName),
         app_id = tostring(initiatedByJson.app.id),
         app_displayName = tostring(initiatedByJson.app.displayName)
| where user_principalName == "badactor@cthfm.com"  // Filter on user
| summarize count() by LoggedByService ActivityDisplayName
</code></pre>

### 3. Associated User Agents

```kusto
AuditLogs
| where isnotempty(AdditionalDetails)  // Ensure field is not null
| extend detailsJson = parse_json(tostring(AdditionalDetails))  // Parse additionalDetails as JSON array
| mv-expand detailsJson  // Expand each object in the array
| where detailsJson["key"] == "User-Agent"  // Keep only the User-Agent key
| extend UserAgent = tostring(detailsJson["value"])  // Extract the value properly
| extend initiatedByJson = parse_json(InitiatedBy)  // Parse InitiatedBy JSON
| extend user_id = tostring(initiatedByJson.user.id), // Parse user id value
         user_displayName = tostring(initiatedByJson.user.displayName), //parse user displayname
         user_principalName = tostring(initiatedByJson.user.userPrincipalName), // parse user principal name
         app_id = tostring(initiatedByJson.app.id), // parse app id
         app_displayName = tostring(initiatedByJson.app.displayName) // parse app display name
| where user_principalName == "badactor@cthfm.com" 
| summarize count() by UserAgent
```

### 4. Resource Interactions:

```kusto
AuditLogs
| where isnotempty(TargetResources)  // Ensure field exists
| extend resourcesJson = parse_json(tostring(TargetResources))  // Convert JSON array
| mv-expand resourcesJson  // Expand each object in the array
| extend 
    resource_userPrincipalName = tostring(resourcesJson.userPrincipalName),
    modifiedProperties = tostring(resourcesJson.modifiedProperties),
    type = tostring(resourcesJson.type) // Extract modifiedProperties array
| extend initiatedByJson = parse_json(InitiatedBy)  // Parse InitiatedBy JSON
| extend user_id = tostring(initiatedByJson.user.id), // Parse user id value
         user_displayName = tostring(initiatedByJson.user.displayName), //parse user displayname
         user_principalName = tostring(initiatedByJson.user.userPrincipalName), // parse user principal name
         app_id = tostring(initiatedByJson.app.id), // parse app id
         app_displayName = tostring(initiatedByJson.app.displayName) // parse app display name
| where user_principalName == "badactor@cthfm.com" 
| summarize count() by user_principalName, type, resource_userPrincipalName, modifiedProperties
```

### Resources:

Helpful Reference for Services:

{% embed url="https://learn.microsoft.com/en-us/entra/identity/monitoring-health/reference-audit-activities" %}
