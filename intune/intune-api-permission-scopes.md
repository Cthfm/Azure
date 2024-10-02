# Intune API Permission Scopes

## Intune permission scopes <a href="#intune-permission-scopes" id="intune-permission-scopes"></a>

Microsoft Entra ID and Microsoft Graph use permission scopes to control access to corporate resources.

Permission scopes (also called the _OAuth scopes_) control access to specific Intune entities and their properties. This section summarizes the permission scopes for Intune API features.

To learn more:

* [Microsoft Entra authentication](https://learn.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication)
* [Application permission scopes](https://learn.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)

When you grant permission to Microsoft Graph, you can specify the following scopes to control access to Intune features: The following table summarizes the Intune API permission scopes. The first column shows the name of the feature as displayed in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and the second column provides the permission scope name.

Expand table

| _Enable Access_ setting                                               | Scope name                                                                                                                                 |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Perform user-impacting remote actions on Microsoft Intune devices** | [DeviceManagementManagedDevices.PrivilegedOperations.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#mgd-po) |
| **Read and write Microsoft Intune devices**                           | [DeviceManagementManagedDevices.ReadWrite.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#mgd-rw)            |
| **Read Microsoft Intune devices**                                     | [DeviceManagementManagedDevices.Read.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#mgd-ro)                 |
| **Read and write Microsoft Intune RBAC settings**                     | [DeviceManagementRBAC.ReadWrite.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#rac-rw)                      |
| **Read Microsoft Intune RBAC settings**                               | DeviceManagementRBAC.Read.All                                                                                                              |
| **Read and write Microsoft Intune apps**                              | [DeviceManagementApps.ReadWrite.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#app-rw)                      |
| **Read Microsoft Intune apps**                                        | [DeviceManagementApps.Read.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#app-ro)                           |
| **Read and write Microsoft Intune Device Configuration and Policies** | DeviceManagementConfiguration.ReadWrite.All                                                                                                |
| **Read Microsoft Intune Device Configuration and Policies**           | [DeviceManagementConfiguration.Read.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#cfg-ro)                  |
| **Read and write Microsoft Intune configuration**                     | [DeviceManagementServiceConfig.ReadWrite.All](https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis#svc-rw)             |
| **Read Microsoft Intune configuration**                               | DeviceManagementServiceConfig.Read.All                                                                                                     |

The table lists the settings as they appear in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The following sections describe the scopes in alphabetical order.

At this time, all Intune permission scopes require administrator access. This means you need corresponding credentials when running apps or scripts that access Intune API resources.

### DeviceManagementApps.Read.All <a href="#app-ro" id="app-ro"></a>

* **Enable Access** setting: **Read Microsoft Intune apps**
* Permits read access to the following entity properties and status:
  * Client Apps
  * Mobile App Categories
  * App Protection Policies
  * App Configurations

### DeviceManagementApps.ReadWrite.All <a href="#app-rw" id="app-rw"></a>

* **Enable Access** setting: **Read and write Microsoft Intune apps**
* Allows the same operations as **DeviceManagementApps.Read.All**
* Also permits changes to the following entities:
  * Client Apps
  * Mobile App Categories
  * App Protection Policies
  * App Configurations

### DeviceManagementConfiguration.Read.All <a href="#cfg-ro" id="cfg-ro"></a>

* **Enable Access** setting: **Read Microsoft Intune device configuration and policies**
* Permits read access to the following entity properties and status:
  * Device Configuration
  * Device Compliance Policy
  * Notification Messages

### DeviceManagementConfiguration.ReadWrite.All <a href="#cfg-ra" id="cfg-ra"></a>

* **Enable Access** setting: **Read and write Microsoft Intune device configuration and policies**
* Allows the same operations as **DeviceManagementConfiguration.Read.All**
* Apps can also create, assign, delete, and change the following entities:
  * Device Configuration
  * Device Compliance Policy
  * Notification Messages

### DeviceManagementManagedDevices.PrivilegedOperations.All <a href="#mgd-po" id="mgd-po"></a>

* **Enable Access** setting: **Perform user-impacting remote actions on Microsoft Intune devices**
* Permits the following remote actions on a managed device:
  * Retire
  * Wipe
  * Reset/Recover Passcode
  * Remote Lock
  * Enable/Disable Lost Mode
  * Clean PC
  * Reboot
  * Delete User from Shared Device

### DeviceManagementManagedDevices.Read.All <a href="#mgd-ro" id="mgd-ro"></a>

* **Enable Access** setting: **Read Microsoft Intune devices**
* Permits read access to the following entity properties and status:
  * Managed Device
  * Device Category
  * Detected App
  * Remote actions
  * Malware information

### DeviceManagementManagedDevices.ReadWrite.All <a href="#mgd-rw" id="mgd-rw"></a>

* **Enable Access** setting: **Read and write Microsoft Intune devices**
* Allows the same operations as **DeviceManagementManagedDevices.Read.All**
* Apps can also create, delete, and change the following entities:
  * Managed Device
  * Device Category
* The following remote actions are also allowed:
  * Locate devices
  * Disable Activation Lock
  * Request remote assistance

### DeviceManagementRBAC.Read.All <a href="#rac-ro" id="rac-ro"></a>

* **Enable Access** setting: **Read Microsoft Intune RBAC settings**
* Permits read access to the following entity properties and status:
  * Role Assignments
  * Role Definitions
  * Resource Operations

### DeviceManagementRBAC.ReadWrite.All <a href="#rac-rw" id="rac-rw"></a>

* **Enable Access** setting: **Read and write Microsoft Intune RBAC settings**
* Allows the same operations as **DeviceManagementRBAC.Read.All**
* Apps can also create, assign, delete, and change the following entities:
  * Role Assignments
  * Role Definitions

### DeviceManagementServiceConfig.Read.All <a href="#svc-ro" id="svc-ro"></a>

* **Enable Access** setting: **Read Microsoft Intune configuration**
* Permits read access to the following entity properties and status:
  * Device Enrollment
  * Apple Push Notification Certificate
  * Apple Device Enrollment Program
  * Apple Volume Purchase Program
  * Exchange Connector
  * Terms and Conditions
  * Cloud PKI
  * Branding
  * Mobile Threat Defense

### DeviceManagementServiceConfig.ReadWrite.All <a href="#svc-rw" id="svc-rw"></a>

* **Enable Access** setting: **Read and write Microsoft Intune configuration**
* Allows the same operations as DeviceManagementServiceConfig.Read.All\_
* Apps can also configure the following Intune features:
  * Device Enrollment
  * Apple Push Notification Certificate
  * Apple Device Enrollment Program
  * Apple Volume Purchase Program
  * Exchange Connector
  * Terms and Conditions
  * Cloud PKI
  * Branding
  * Mobile Threat Defense

### Reference

{% embed url="https://learn.microsoft.com/en-us/mem/intune/developer/intune-graph-apis" %}

