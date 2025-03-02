# PCAP Acquisition

### Overview:&#x20;

Azure Network Watcher is a network monitoring and diagnostic service designed to provide insights into network performance, connectivity, and security within Azure environments. One of its key features is Packet Capture, which allows users to collect network traffic data from Azure Virtual Machines (VMs) and Virtual Machine Scale Sets (VMSS) for analysis and troubleshooting.&#x20;

To obtain a PCAP (packet capture) in Azure, follow these steps:

### **1. Enable Network Watcher**

Azure provides a built-in tool called **Azure Network Watcher** that allows you to capture network traffic.

* In the Azure portal, search for Network Watcher.
* Select the Network Watcher instance for your region.
* Enable it if it is not already enabled.

## **2. Start a Packet Capture - Azure Portal**

You can start a packet capture on an Azure Virtual Machine (VM) using **Azure Network Watcher**.

**Using the Azure Portal**

1. Navigate to **Network Watcher** → **Packet Capture**.
2. Click **+ Add** to start a new capture.
3. Select the target VM in the respective subscription and resource group
4. Configure:
   * **Packet Capture Name**: Provide a name for the capture session.
   * **Storage Account** (Optional): You can save the packet capture in an Azure Storage Account.
   * **File Path** (Optional): Specify a local file path on the VM (e.g., `/var/log/capture.pcap` for Linux or `C:\captures\capture.pcap` for Windows).
   * **Filters (Optional)**: Set up filters such as:
     * **Protocol** (TCP, UDP, ICMP)
     * **Source IP/Port**
     * **Destination IP/Port**
     * **Packet Size Limit** (Set a limit on the number of bytes per packet)
5. Click **Start**.

### **3. Start a Packet Capture - Using Azure CLI**

Alternatively, you can use the **Azure CLI**:

```sh
az network watcher packet-capture create \
  --resource-group <Resource-Group> \
  --network-watcher-name <Network-Watcher-Name> \
  --vm <VM-Name> \
  --name <Capture-Name> \
  --storage-account <Storage-Account-Name> \
  --filters "[{protocol: 'TCP', remotePort: '80'}]"
```

This command will start capturing TCP traffic on port 80.

### **4. Stop the Packet Capture - Azure CLI**

To stop an active capture using Azure CLI:

```sh
az network watcher packet-capture stop \
  --resource-group <Resource-Group> \
  --network-watcher-name <Network-Watcher-Name> \
  --name <Capture-Name>
```

### **5. Download and Analyze the PCAP - Azure CLI**

Once the capture is completed:

* If stored in Azure Storage, navigate to the storage account and download the `.pcap` file.
* If stored on the VM, use RDP/SSH to retrieve the file.

You can analyze the `.pcap` file using **Wireshark** or **tcpdump**:

```sh
tcpdump -r capture.pcap
```

#### **Additional Considerations**

* **Network Security Groups (NSGs)**: Ensure your NSGs allow the traffic you intend to capture.
* **Capture Storage Limits**: The maximum size for a capture is **1 GB** per session.
* **Retention**: Azure does not retain PCAP files indefinitely; download them promptly or ensure you have a proper data retention lifecycle in place.&#x20;

### **6. List Active Packet Captures - AZ CLI**

To see active packet capture sessions:

```bash
az network watcher packet-capture list --resource-group MyResourceGroup
```

### **7. Stop a Packet Capture Session - AZ CLI**

To stop a running packet capture:

```bash
az network watcher packet-capture stop \
  --name MyPacketCapture \
  --resource-group MyResourceGroup
```

### AZ CLI Reference

{% embed url="https://learn.microsoft.com/en-us/cli/azure/network/watcher/packet-capture?view=azure-cli-latest" %}

### Azure Documentation: Managing Packet Captures

{% embed url="https://learn.microsoft.com/en-us/azure/network-watcher/packet-capture-manage?tabs=portal" %}
