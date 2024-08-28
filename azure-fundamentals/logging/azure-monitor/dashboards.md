# Dashboards

## Overview:

Azure Monitor dashboards provide a powerful way to visualize and monitor the health, performance, and security of your Azure resources. This step-by-step guide is designed for beginners who are new to creating dashboards in Azure Monitor.

### **Prerequisites**

* An active Azure subscription.
* Basic knowledge of Azure services (e.g., Virtual Machines, Storage Accounts).

### **Step 1: Accessing Azure Monitor**

1. **Log in to the Azure Portal:**
   * Go to [portal.azure.com](https://portal.azure.com).
   * Use your Azure credentials to log in.
2. **Navigate to Azure Monitor:**
   * In the Azure Portal, search for **"Azure Monitor"** in the top search bar and select it from the results.
   * This will take you to the Azure Monitor overview page, where you can see insights into your resources.

### **Step 2: Create a New Dashboard**

1. **Access the Dashboard Blade:**
   * On the left-hand side menu, select **"Dashboard"**.
   * Click on **"New dashboard"** at the top left of the dashboard pane.
2. **Name Your Dashboard:**
   * In the **"New dashboard"** pane, enter a meaningful name for your dashboard. For example, **"Resource Performance Monitor"**.
   * Choose whether you want it to be a private dashboard (only visible to you) or shared (visible to others with appropriate access).

### **Step 3: Adding Resources to Your Dashboard**

1. **Add Tiles:**
   * A blank grid will appear where you can add tiles. Tiles are individual widgets that display different types of data.
   * On the right-hand side, click on **"Add tile"** to see available visualizations (e.g., charts, grids, maps).
2. **Select Data to Visualize:**
   * You can add metrics, logs, or alerts from your resources.
   * For example, to add a performance chart for a Virtual Machine:
     * Click on **"Metrics"**.
     * Choose the resource type (e.g., **"Virtual Machines"**).
     * Select a specific Virtual Machine.
     * Choose a metric to display (e.g., **"Percentage CPU"**).
     * Configure the time range, aggregation type (average, sum, etc.), and visualization style (line chart, bar chart, etc.).
     * Click **"Apply"** to add it to the dashboard.
3. **Customize the Tile Layout:**
   * Resize and reposition tiles by dragging the corners or moving them across the grid.
   * Add more tiles as needed, such as activity logs, alerts, or custom queries from Azure Monitor Logs.

### **Step 4: Customizing Your Dashboard**

1. **Configure Tile Settings:**
   * Click on the ellipsis (**...**) on a tile to open its settings.
   * You can modify the metric, visualization style, or even change the resource it is monitoring.
2. **Add Filters:**
   * Apply filters to your dashboard to focus on specific resources or regions.
   * Click on **"Edit"** at the top of the dashboard, then select **"Add a filter"**.
   * Choose a filter (e.g., Resource Group) to narrow down the data displayed across the entire dashboard.
3. **Add Custom Queries:**
   * If you are familiar with Kusto Query Language (KQL), you can create custom log queries in Azure Monitor Logs and pin the results to your dashboard.

### **Step 5: Save and Share Your Dashboard**

1. **Save Your Dashboard:**
   * Once you’re satisfied with the layout and content, click **"Save"** at the top of the dashboard.
   * Your dashboard is now available for monitoring and can be accessed anytime from the **"Dashboard"** section in the Azure Portal.
2. **Share the Dashboard:**
   * If you chose to create a shared dashboard, you can manage access by clicking on **"Share"** at the top.
   * Assign roles and permissions to others in your organization to view or edit the dashboard.

### **Step 6: Continuous Monitoring and Updates**

1. **Regularly Update Your Dashboard:**
   * As your environment grows or changes, revisit your dashboard to add new tiles or modify existing ones.
   * Keep the dashboard relevant by incorporating new metrics or resources that are critical to your operations.
2. **Set Up Alerts:**
   * Enhance your dashboard by setting up alerts in Azure Monitor that trigger when certain conditions are met (e.g., CPU usage exceeds 80%).
   * Pin alerts to your dashboard to quickly see ongoing issues.
3. **Use Azure Monitor Workbooks:**
   * For more complex visualizations and analyses, consider using **Azure Monitor Workbooks**. They provide more customization options and can be pinned to dashboards.
