# Log Retention Strategies

### Overview

In Azure, you can extend the retention of logs using three primary methods:

1. **Exporting Logs to a Storage Account**
2. **Sending Logs to a Log Analytics Workspace**
3. **Streaming Logs to an Event Hub**

Here's an overview of each method and how they can be used to extend the retention of logs:

### 1. Exporting Logs to a Storage Account

Exporting logs to a storage account allows you to archive them for longer periods. This method is suitable for long-term storage and compliance purposes.

**Advantages:**

* Cost-effective for long-term storage.
* Easy access to raw log data for analysis and auditing.

**How to Configure:**

**Using Azure Portal:**

1. **Open Azure Portal** and navigate to the service you want to configure (e.g., Activity Logs, Azure AD Logs, Resource Logs).
2. **Add Diagnostic Setting:**
   * For Activity Logs: Go to `Azure Monitor > Activity Log > Export Activity Logs > + Add diagnostic setting`.
   * For Azure AD Logs: Go to `Azure Active Directory > Audit logs` or `Sign-ins > Export Data Settings > + Add diagnostic setting`.
   * For Resource Logs: Go to the specific resource (e.g., Virtual Machine) > `Monitoring > Diagnostic settings > + Add diagnostic setting`.
3. **Configure Diagnostic Setting:**
   * Name your diagnostic setting.
   * Select `Archive to a storage account` and choose your storage account.
4. **Save Configuration**.

**Using Azure CLI:**

```bash
az monitor diagnostic-settings create \
  --name "LogExportToStorage" \
  --resource "<resource-id>" \
  --logs '[{"category": "Administrative", "enabled": true}]' \
  --storage-account "/subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group>/providers/Microsoft.Storage/storageAccounts/<your-storage-account>"
```

### 2. Sending Logs to a Log Analytics Workspace

Sending logs to a Log Analytics workspace allows you to perform advanced queries, set up alerts, and analyze logs using Azure Monitor.

**Advantages:**

* Advanced querying and analytics capabilities.
* Integration with Azure Monitor and other Azure services.
* Configurable retention up to 730 days or more.

**How to Configure:**

**Using Azure Portal:**

1. **Open Azure Portal** and navigate to the service you want to configure (e.g., Activity Logs, Azure AD Logs, Resource Logs).
2. **Add Diagnostic Setting:**
   * For Activity Logs: Go to `Azure Monitor > Activity Log > Export Activity Logs > + Add diagnostic setting`.
   * For Azure AD Logs: Go to `Azure Active Directory > Audit logs` or `Sign-ins > Export Data Settings > + Add diagnostic setting`.
   * For Resource Logs: Go to the specific resource (e.g., Virtual Machine) > `Monitoring > Diagnostic settings > + Add diagnostic setting`.
3. **Configure Diagnostic Setting:**
   * Name your diagnostic setting.
   * Select `Send to Log Analytics workspace` and choose your Log Analytics workspace.
4. **Save Configuration**.

**Using Azure CLI:**

```bash
az monitor diagnostic-settings create \
  --name "LogExportToLogAnalytics" \
  --resource "<resource-id>" \
  --logs '[{"category": "Administrative", "enabled": true}]' \
  --workspace "/subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group>/providers/Microsoft.OperationalInsights/workspaces/<your-workspace>"
```

### 3. Streaming Logs to an Event Hub

Streaming logs to an Event Hub enables integration with external systems and real-time processing of log data.

**Advantages:**

* Real-time log processing.
* Integration with external systems like SIEMs (Security Information and Event Management).
* Scalability for large volumes of data.

**How to Configure:**

**Using Azure Portal:**

1. **Open Azure Portal** and navigate to the service you want to configure (e.g., Activity Logs, Azure AD Logs, Resource Logs).
2. **Add Diagnostic Setting:**
   * For Activity Logs: Go to `Azure Monitor > Activity Log > Export Activity Logs > + Add diagnostic setting`.
   * For Azure AD Logs: Go to `Azure Active Directory > Audit logs` or `Sign-ins > Export Data Settings > + Add diagnostic setting`.
   * For Resource Logs: Go to the specific resource (e.g., Virtual Machine) > `Monitoring > Diagnostic settings > + Add diagnostic setting`.
3. **Configure Diagnostic Setting:**
   * Name your diagnostic setting.
   * Select `Stream to an event hub` and choose your Event Hub namespace and Event Hub name.
4. **Save Configuration**.

**Using Azure CLI:**

```bash
az monitor diagnostic-settings create \
  --name "LogExportToEventHub" \
  --resource "<resource-id>" \
  --logs '[{"category": "Administrative", "enabled": true}]' \
  --event-hub "/subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group>/providers/Microsoft.EventHub/namespaces/<your-event-hub-namespace>/eventhubs/<your-event-hub>"
```
