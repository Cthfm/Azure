# Provisioning Logs (AADProvisioningLogs)

## Provisioning Logs Overview:

Azure provides a feature that allows identities to be created. This is called, identity provisioning.&#x20;

Identity provisioning is the automated process of creating, managing, and deactivating user accounts and other digital identities within an organization's IT ecosystem. It ensures that users have the necessary access to applications and resources, whether on-premises or in the cloud, based on predefined conditions.

For example, when a new employee joins a company, their information is entered into the Human Resources (HR) system. Identity provisioning then automatically creates corresponding user accounts across various platforms, such as Active Directory, cloud applications like Microsoft Entra ID, and other necessary services. This process enables the employee to access required applications and systems from day one.

Identity provisioning can be categorized into several key scenarios:

1. **HR-Driven Provisioning**: Automatically creates, updates, or disables user accounts based on changes in the HR system. For instance, when an employee is hired, their account is created across multiple platforms, or when they leave, their access is disabled.
2. **App Provisioning**: Involves the creation and management of user identities and roles within cloud applications. For example, provisioning a Microsoft Entra user into applications like Dropbox or Salesforce as needed.
3. **Directory Provisioning**: Refers to provisioning user accounts from on-premises sources, like Active Directory, into cloud directories such as Microsoft Entra ID.

### Schema:

| Column                 | Type     | Description                                                                                                                                                                                            |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| AADTenantId            | string   | Unique Azure AD tenant ID                                                                                                                                                                              |
| \_BilledSize           | real     | The record size in bytes                                                                                                                                                                               |
| Category               | string   | Category of the event                                                                                                                                                                                  |
| ChangeId               | string   | Unique ID of this change in this cycle                                                                                                                                                                 |
| CorrelationId          | string   | ID to provide provisioning trail                                                                                                                                                                       |
| CycleId                | string   | Unique ID per job iteration                                                                                                                                                                            |
| DurationMs             | long     | Indicates how long this provisioning action took to finish                                                                                                                                             |
| Id                     | string   | Indicates the unique ID for the activity                                                                                                                                                               |
| InitiatedBy            | string   | Details of who initiated this provisioning                                                                                                                                                             |
| \_IsBillable           | string   | Specifies whether ingesting the data is billable. When \_IsBillable is `false` ingestion isn't billed to your Azure account                                                                            |
| JobId                  | string   | The unique ID for the whole provisioning job                                                                                                                                                           |
| ModifiedProperties     | string   | Details of each property that was modified in this provisioning action on this object                                                                                                                  |
| OperationName          | string   | Name of the operation                                                                                                                                                                                  |
| OperationVersion       | string   | The REST API version that's requested by the client                                                                                                                                                    |
| ProvisioningAction     | string   | Indicates the activity name or the operation name. For a list of activities logged, refer to Azure AD activity list                                                                                    |
| ProvisioningStatusInfo | string   | Details of provisioning status                                                                                                                                                                         |
| ProvisioningSteps      | string   | Details of each step in provisioning                                                                                                                                                                   |
| ResultDescription      | string   | When available, provides the error description for the provisioning operation                                                                                                                          |
| ResultSignature        | string   | Contains the error code, if any, for the provisioning operation                                                                                                                                        |
| ResultType             | string   | The result of the provisioning operation can be Success, Failure, or Skipped                                                                                                                           |
| ServicePrincipal       | string   | Represents the service principal used for provisioning                                                                                                                                                 |
| SourceIdentity         | string   | Details of source object being provisioned                                                                                                                                                             |
| SourceSystem           | string   | The type of agent the event was collected by. For example, `OpsManager` for Windows agent, either direct connect or Operations Manager, `Linux` for all Linux agents, or `Azure` for Azure Diagnostics |
| TargetIdentity         | string   | Details of target object being provisioned                                                                                                                                                             |
| TargetSystem           | string   | Details of target system of the object being provisioned                                                                                                                                               |
| TenantId               | string   | The Log Analytics workspace ID                                                                                                                                                                         |
| TimeGenerated          | datetime | The date and time of the event in UTC                                                                                                                                                                  |
| Type                   | string   | The name of the table                                                                                                                                                                                  |

### Table Reference:

{% embed url="https://learn.microsoft.com/en-us/azure/azure-monitor/reference/tables/aadprovisioninglogs" %}
