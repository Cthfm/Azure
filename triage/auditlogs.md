---
hidden: true
---

# Azure Activity Logs

## Overview:

The following are some basic KQL commands to do principal-based triage. These can be setup in a logic app or automation to be run whenever an alert in Sentinel or your SIEM fires.&#x20;



{% hint style="danger" %}
These are merely ideas and can be developed to meet your organization needs.
{% endhint %}



1. ### Overview Search

This search will show the overview of the user or app activities with key fields.

````

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
````

2. Services and Operations Completed by the Application or User

This shows the services that the user or application interacted with and the associated count. This gives us the scope of the activity within a given time frame.

```
AuditLogs|
extend initiatedByJson = parse_json(InitiatedBy)  // Parse InitiatedBy JSON
| extend user_id = tostring(initiatedByJson.user.id),
         user_displayName = tostring(initiatedByJson.user.displayName),
         user_principalName = tostring(initiatedByJson.user.userPrincipalName),
         app_id = tostring(initiatedByJson.app.id),
         app_displayName = tostring(initiatedByJson.app.displayName)
| where user_principalName == "badactor@cthfm.com"  // Filter on user
| summarize count() by LoggedByService ActivityDisplayName
```

3.
