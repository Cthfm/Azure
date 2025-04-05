# Monitoring and Troubleshooting in Azure CLI

## 📖 8.1 Why Monitor Azure Resources?

Monitoring helps you:

| Benefit              | Why It’s Important                          |
| -------------------- | ------------------------------------------- |
| Detect issues early  | Spot problems before they cause downtime    |
| Optimize performance | Track resource usage and adjust accordingly |
| Improve security     | Detect suspicious activities                |
| Audit changes        | Track who made what changes and when        |

✅ Monitoring is **proactive** — it’s the key to maintaining a healthy Azure environment!

***

## 📜 8.2 Viewing Activity Logs with Azure CLI

The **Activity Log** records operations on resources at the **control plane** (e.g., resource creation, deletion).

***

#### 🛠️ View Recent Activity Logs

```bash
bashCopyEditaz monitor activity-log list --output table
```

✅ Displays recent activities like create, delete, and update operations.

***

#### Filter by Resource Group

```bash
bashCopyEditaz monitor activity-log list \
  --resource-group myResourceGroup \
  --output table
```

✅ Only shows activity in a specific Resource Group.

***

#### Filter by Time

Get logs from the past hour:

```bash
bashCopyEditaz monitor activity-log list --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%SZ) --output table
```

✅ Useful for investigating **recent changes**.

***

## 📊 8.3 Viewing Metrics for Resources

Azure **Metrics** provide near real-time data on resource performance.

***

#### 🛠️ List Available Metrics for a VM

```bash
bashCopyEditaz monitor metrics list-definitions \
  --resource /subscriptions/<sub-id>/resourceGroups/<rg-name>/providers/Microsoft.Compute/virtualMachines/<vm-name> \
  --output table
```

✅ Shows all available metrics for the VM (CPU usage, Disk IO, etc.).

***

#### 🛠️ Get CPU Usage Metrics

```bash
bashCopyEditaz monitor metrics list \
  --resource /subscriptions/<sub-id>/resourceGroups/<rg-name>/providers/Microsoft.Compute/virtualMachines/<vm-name> \
  --metric "Percentage CPU" \
  --interval PT1M \
  --output table
```

| TimeStamp            | Average |
| -------------------- | ------- |
| 2025-04-05T14:00:00Z | 12.5    |
| 2025-04-05T14:01:00Z | 14.2    |

✅ See how busy your VM is!

***

## 🩺 8.4 Diagnosing Virtual Machine Issues

When VMs act weird (fail to boot, slow down, crash), **diagnostics** are your friend.

***

#### 🛠️ Enable Boot Diagnostics

```bash
bashCopyEditaz vm boot-diagnostics enable \
  --resource-group myResourceGroup \
  --name myVM
```

✅ Captures screenshots and logs during VM startup.

***

#### 🛠️ View Boot Diagnostics Info

```bash
bashCopyEditaz vm boot-diagnostics get-boot-log \
  --resource-group myResourceGroup \
  --name myVM
```

✅ See the **boot log** and **screenshot** to help diagnose issues.

***

## ⚙️ 8.5 Configuring Diagnostics Settings

Azure resources can send logs and metrics to:

* Log Analytics Workspace
* Storage Account
* Event Hub

✅ You can set this up with Azure CLI too!

***

#### 🛠️ Example: Send Diagnostics to a Log Analytics Workspace

```bash
bashCopyEditaz monitor diagnostic-settings create \
  --name myDiagnosticsSetting \
  --resource /subscriptions/<sub-id>/resourceGroups/<rg-name>/providers/Microsoft.Compute/virtualMachines/<vm-name> \
  --workspace <workspace-id> \
  --metrics '[{"category": "AllMetrics","enabled": true}]' \
  --logs '[{"category": "Administrative","enabled": true}]'
```

✅ Centralized logging = easier troubleshooting!

***

## 🔥 8.6 Real-World Troubleshooting Example

Problem:\
You can't connect to your new Linux VM.

✅ Here’s a basic troubleshooting flow:

| Step | CLI Command                           | Purpose                                 |
| ---- | ------------------------------------- | --------------------------------------- |
| 1    | `az vm show`                          | Verify VM exists and is running         |
| 2    | `az network nic show`                 | Check NIC (network interface) status    |
| 3    | `az network nsg rule list`            | Verify NSG allows SSH inbound (port 22) |
| 4    | `az vm boot-diagnostics get-boot-log` | Check if VM booted properly             |

If SSH port is blocked or the VM failed to boot — **you’ll know fast**.

***

## 🛡️ 8.7 Best Practices for Monitoring and Troubleshooting

| Best Practice                       | Why It Matters                            |
| ----------------------------------- | ----------------------------------------- |
| Enable diagnostics from the start   | Avoid scrambling during incidents         |
| Send logs to Log Analytics          | Centralized monitoring and analysis       |
| Regularly review Activity Logs      | Detect unauthorized or suspicious changes |
| Monitor key metrics (CPU, Disk)     | Avoid outages from resource exhaustion    |
| Script common troubleshooting tasks | Save time during incidents                |

***

## 📝 Module 8 Summary

| Topic                          | Key Points                                    |
| ------------------------------ | --------------------------------------------- |
| View Activity Logs             | `az monitor activity-log list`                |
| Monitor Metrics                | `az monitor metrics list`                     |
| Diagnose VMs                   | Boot diagnostics help fix startup problems    |
| Configure Diagnostics Settings | Send logs/metrics to centralized locations    |
| Troubleshooting best practices | Proactive monitoring saves time and resources |
