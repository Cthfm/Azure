# Workbooks

## Workbook Overview

Azure Workbooks are interactive, customizable reports that help security analysts visualize and analyze security-related data. Workbooks can aggregate data from multiple sources, allowing analysts to identify patterns, investigate anomalies, and respond to security threats more effectively.

### Key Features of Workbooks

1. **Data Integration**: Pull in data from Log Analytics, Azure Security Center, Azure Sentinel, and other data sources.
2. **Querying Capabilities**: Use Kusto Query Language (KQL) to write complex queries for detailed data analysis.
3. **Flexible Visualizations**: Create charts, tables, and graphs to visualize data effectively.
4. **Templates**: Leverage pre-built templates for common security scenarios and customize them as needed.

### Workbook Setup

**Step 1: Access Azure Monitor**

1. **Log in to Azure Portal**: Go to [Azure Portal](https://portal.azure.com) and log in with your credentials.
2. **Navigate to Azure Monitor**: Use the search bar at the top to search for "Azure Monitor" and select it from the results.

**Step 2: Open Workbooks**

1. **Go to Workbooks**: In the Azure Monitor overview pane, select **Workbooks** under the **Insights** section.

**Step 3: Create a New Workbook**

1. **Create a New Workbook**:
   * Click on the **New** button to start creating a new workbook.

**Step 4: Add and Customize Content**

1. **Add a Text Block**:
   * Click on the **Add** button and select **Text**.
   * Use this block to add descriptions, titles, or any textual content.
   * Example: Title: "Security Event Monitoring", Description: "This workbook provides insights into security-related events."
2. **Add a Query Control for Failed Logins**:
   * Click on the **Add** button and select **Query**.
   * Select the data source (e.g., Log Analytics) and write your KQL query to fetch the data.
   *   Example Query:

       ```kusto
       SecurityEvent
       | where EventID == 4625
       | summarize count() by bin(TimeGenerated, 1h), Account
       ```
   * Visualize this data using a time chart to show failed login attempts over time.
3. **Add a Query Control for Successful Logins**:
   *   Add another query block with this KQL query:

       ```kusto
       SecurityEvent
       | where EventID == 4624
       | summarize count() by bin(TimeGenerated, 1h), Account
       ```
   * Visualize this data using a bar chart to show successful login attempts.
4. **Add a Query Control for High-Severity Alerts**:
   *   Add a query block with this KQL query:

       ```kusto
       SecurityAlert
       | where Severity == "High"
       | summarize count() by bin(TimeGenerated, 1h), AlertName
       ```
   * Visualize this data using a pie chart to show the distribution of high-severity alerts.
5. **Add Parameters for Filtering**:
   * Click on the **Add** button and select **Parameter** to create dynamic inputs for your queries.
   * Define the parameter type (e.g., dropdown for time range, text box for specific account names) and link it to your queries.

#### **Step 5: Configure and Customize Workbook**

1. **Arrange and Format**:
   * Drag and drop the elements to arrange them in your workbook.
   * Use the formatting options to customize the appearance of your text, queries, and visualizations.
2. **Save the Workbook**:
   * Click on the **Save** button.
   * Provide a name, description, and save it in a specific resource group or subscription.

#### **Step 6: Share and Collaborate**

1. **Set Permissions**:
   * Go to the **Access Control (IAM)** section of your workbook and configure permissions to share the workbook with your team.
2. **Share Link**:
   * You can also share the workbook by providing a direct link to it within the Azure Portal.

### Example Security Event Workbook Scenario

Let’s create a basic workbook to monitor security events like failed logins, successful logins, and high-severity alerts.

1. **Add Text**:
   * Add a title "Security Event Monitoring" and a description: "This workbook provides insights into failed and successful login attempts, as well as high-severity security alerts."
2. **Add Failed Login Attempts Query**:
   *   Add a query block and use the following KQL query:

       ```kusto
       SecurityEvent
       | where EventID == 4625
       | summarize count() by bin(TimeGenerated, 1h), Account
       ```
   * Visualize this data using a time chart.
3. **Add Successful Login Attempts Query**:
   *   Add another query block with this KQL query:

       ```kusto
       SecurityEvent
       | where EventID == 4624
       | summarize count() by bin(TimeGenerated, 1h), Account
       ```
   * Visualize this data using a bar chart.
4. **Add High-Severity Alerts Query**:
   *   Add another query block with this KQL query:

       ```kusto
       SecurityAlert
       | where Severity == "High"
       | summarize count() by bin(TimeGenerated, 1h), AlertName
       ```
   * Visualize this data using a pie chart.
5. **Save and Share**:
   * Save the workbook and share it with your team.
