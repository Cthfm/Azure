# Setup

## Setup Log Analytics Workspace

The following section provides steps on how to setup a Log Analytics workspace in an Azure Tenant

### **Step 1: Sign in to the Azure Portal**

1. **Open the Azure Portal:**
   * Go to [https://portal.azure.com](https://portal.azure.com) in your web browser.
   * Sign in with your Azure account credentials.

### **Step 2: Navigate to Log Analytics Workspaces**

1. **Access Log Analytics Workspaces:**
   * In the Azure portal, click on the search bar at the top and type "Log Analytics Workspaces."
   * Select "Log Analytics Workspaces" from the search results.

### **Step 3: Create a New Log Analytics Workspace**

1. **Start Workspace Creation:**
   * Click on the "+ Create" button at the top left corner of the Log Analytics Workspaces page.
2. **Configure Basic Settings:**
   * **Subscription:** Select the subscription where you want to create the workspace.
   * **Resource Group:** Choose an existing resource group or create a new one by clicking on "Create new."
   * **Name:** Enter a unique name for your Log Analytics workspace.
   * **Region:** Select the region where you want to create the workspace. Choose a region that is geographically close to your resources to minimize latency.
3. **Review and Create:**
   * Click on the "Review + create" button at the bottom of the page.
   * Review the workspace configuration details.
   * Click on "Create" to create the Log Analytics workspace.

### **Step 4: Configure Data Sources**

1. **Navigate to Your Workspace:**
   * Once the workspace is created, you can find it by going to "Log Analytics Workspaces" in the Azure portal and selecting the newly created workspace.
2. **Connect Data Sources:**
   * **Virtual Machines:**
     * Go to the workspace and click on "Virtual machines" under the "Workspace Data Sources" section.
     * Click on the "Connect" button next to the virtual machines you want to connect.
   * **Azure Resources:**
     * Enable diagnostics and log collection for various Azure resources (e.g., Azure SQL, Azure Storage, Azure AD) by navigating to the resource’s settings and configuring diagnostic settings to send logs to your Log Analytics workspace.
   * **Custom Logs:**
     * You can also collect custom logs by configuring the Custom Logs feature in the Log Analytics workspace.

### **Step 5: Configure Diagnostic Settings for Azure Resources**

1. **Enable Diagnostic Logs:**
   * For each Azure resource, navigate to its settings in the Azure portal.
   * Click on "Diagnostics settings" or "Diagnostic logs."
   * Click on "Add diagnostic setting" or "Add" to create a new diagnostic setting.
2. **Configure Diagnostic Logs:**
   * **Name:** Provide a name for the diagnostic setting.
   * **Logs and Metrics:** Select the logs and metrics you want to collect.
   * **Destination:** Choose "Send to Log Analytics workspace."
   * **Workspace:** Select the subscription and the Log Analytics workspace you created earlier.
3. **Save Settings:**
   * Click "Save" to apply the diagnostic settings.

### **Step 6: Verify Data Collection**

1. **Access Logs:**
   * Navigate to your Log Analytics workspace in the Azure portal.
   * Click on "Logs" under the "General" section.
2. **Run Queries:**
   * Use Kusto Query Language (KQL) to run queries and verify that logs are being collected.
   *   Example query to check for recent logs:

       ```kql
       AzureDiagnostics
       | where TimeGenerated > ago(24h)
       ```
