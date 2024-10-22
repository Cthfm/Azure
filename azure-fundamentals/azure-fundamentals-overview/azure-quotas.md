# Azure Quotas

## Overview

Azure Quotas (also known as _service limits_ or _resource limits_) are predefined limits on the resources you can use in your Azure subscription. They exist to prevent overconsumption, optimize infrastructure management, and ensure fair resource distribution across all users.

Quotas can apply at various levels, including subscriptions, resource groups, and regions, and they differ based on the type of service, such as virtual machines (VMs), storage, networking, or databases. It’s essential to understand and monitor these quotas as they can affect resource provisioning and availability, especially in production environments.

### **Categories of Azure Quotas**

1. **Subscription Quotas**
   * Maximum number of resources a single Azure subscription can use (e.g., 980 resource groups per subscription).
2. **Service-Specific Quotas**
   * Each service may have unique limits. For example:
     * **Virtual Machines:** Max cores per region per subscription.
     * **Azure SQL Database:** Max databases per server.
     * **Storage Accounts:** Max accounts per region per subscription.
3. **Regional Quotas**
   * Limits on the number of resources allowed per region to ensure capacity management across Azure’s global infrastructure.
     * Example: A quota of 250 virtual machines (VM cores) per region.
4. **Resource Group Quotas**
   * Limits on resources within a single resource group (e.g., 800 resources per resource group).

### **Common Azure Quotas by Service**

* **Compute (VMs) Quota:**
  * VM cores: Maximum number of CPU cores across VMs per region.
  * Virtual Machine Scale Sets (VMSS): Max instances per scale set.
* **Storage Quota:**
  * Max blob containers or files within an account.
  * Data capacity limits (e.g., 5 PiB per storage account for some tiers).
* **Networking Quota:**
  * Max public IP addresses per region.
  * Max virtual networks or subnets.
* **Azure SQL Database Quota:**
  * Max DTU (Database Transaction Unit) for elastic pools.
  * Max SQL databases per server.

### **Why Quotas Matter**

* **Capacity Planning:** Ensure resource limits will not hinder service availability, especially in growing environments.
* **Cost Management:** Help you control spending by setting usage thresholds for specific resources.
* **Performance:** Quotas safeguard against unintentional resource overconsumption, maintaining consistent performance.

### **Monitoring and Increasing Quotas**

1.  **View Quotas:**\
    Use the **Azure Portal** or the **Azure CLI** to check quotas:

    ```bash
    az vm list-usage --location eastus --output table
    ```
2. **Request a Quota Increase:**\
   If you need more resources, you can request an increase through the **Azure Portal**:
   * Navigate to **Help + Support** > **Create a Support Request**.
   * Choose **Quota** as the issue type and specify the service and region.
3. **Automating Quota Management:**\
   Use Azure Monitor to create alerts when usage approaches quota limits. This ensures you act before your resources run out.

### Common Service Limits

These are common service limits that are associated with management groups, resource groups, subscriptions, and etc.&#x20;

{% embed url="https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits" %}

### Quota API

Use the Quota API in order to get information on Quota limits programmatically

{% embed url="https://learn.microsoft.com/en-us/rest/api/quota/" %}

### Rest Operation Groups

List of specific operations in context to programmatically querying quota limits, submitting requests for quota increases, and checking the status of quota increases.&#x20;

{% embed url="https://learn.microsoft.com/en-us/rest/api/quota/operation-groups?view=rest-quota-2023-02-01" %}
