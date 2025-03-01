---
hidden: true
---

# PCAP Acquisition

To obtain a PCAP (packet capture) in Azure, follow these steps:

#### **1. Enable Network Watcher**

Azure provides a built-in tool called **Azure Network Watcher** that allows you to capture network traffic.

* In the **Azure portal**, search for **Network Watcher**.
* Select the **Network Watcher** instance for your region.
* Enable it if it is not already enabled.

#### **2. Start a Packet Capture**

You can start a packet capture on an Azure Virtual Machine (VM) using **Azure Network Watcher**.

**Using the Azure Portal**

1. Navigate to **Network Watcher** → **Packet Capture**.
2. Click **+ Add** to start a new capture.
3. Select the target **VM**.
4. Configure:
   * Name of the capture.
   * **Storage location**: Either a local disk on the VM or an Azure Storage account.
   * **Filters**: (Optional) To capture specific traffic types (IP addresses, ports, protocols).
5. Click **Start**.

**Using Azure CLI**

Alternatively, you can use the **Azure CLI**:

```sh
shCopyEditaz network watcher packet-capture create \
  --resource-group <Resource-Group> \
  --network-watcher-name <Network-Watcher-Name> \
  --vm <VM-Name> \
  --name <Capture-Name> \
  --storage-account <Storage-Account-Name> \
  --filters "[{protocol: 'TCP', remotePort: '80'}]"
```

This command will start capturing **TCP traffic on port 80**.

#### **3. Stop the Packet Capture**

To stop an active capture using Azure CLI:

```sh
shCopyEditaz network watcher packet-capture stop \
  --resource-group <Resource-Group> \
  --network-watcher-name <Network-Watcher-Name> \
  --name <Capture-Name>
```

#### **4. Download and Analyze the PCAP**

Once the capture is completed:

* If stored in **Azure Storage**, navigate to the storage account and download the `.pcap` file.
* If stored on the VM, use **RDP/SSH** to retrieve the file.

You can analyze the `.pcap` file using **Wireshark** or **tcpdump**:

```sh
shCopyEdittcpdump -r capture.pcap
```

#### **Additional Considerations**

* **Network Security Groups (NSGs)**: Ensure your NSGs allow the traffic you intend to capture.
* **Capture Storage Limits**: The maximum size for a capture is **1 GB** per session.
* **Retention**: Azure does not retain PCAP files indefinitely; download them promptly.





### **Generating a Packet Capture from the Azure Portal**

1. **Navigate to Network Watcher**
   * Sign in to the [Azure Portal](https://portal.azure.com).
   * In the search bar, type **Network Watcher** and select it from the results.
2. **Select Packet Capture**
   * In the left-hand menu, click on **Packet Capture** under **Monitoring**.
3. **Create a New Packet Capture**
   * Click **+ Add** to create a new packet capture.
   * Select the **Subscription** and **Resource Group** where your target VM is located.
   * Under **Target Virtual Machine**, select the VM on which you want to capture packets.
4. **Configure Packet Capture Settings**
   * **Packet Capture Name**: Provide a name for the capture session.
   * **Storage Account** (Optional): You can save the packet capture in an Azure Storage Account.
   * **File Path** (Optional): Specify a local file path on the VM (e.g., `/var/log/capture.pcap` for Linux or `C:\captures\capture.pcap` for Windows).
   * **Filters (Optional)**: Set up filters such as:
     * **Protocol** (TCP, UDP, ICMP)
     * **Source IP/Port**
     * **Destination IP/Port**
     * **Packet Size Limit** (Set a limit on the number of bytes per packet)
5. **Start Packet Capture**
   * Click **OK** or **Start** to begin the packet capture.
6. **Stop and Download**
   * Let the capture run for the desired duration.
   * Click **Stop** when you are done.
   * If saved in a storage account, download the **.pcap** file for analysis in tools like **Wireshark**.

***

### **Generating a Packet Capture Using Azure CLI**

You can also initiate a packet capture using the Azure CLI.

#### **1. Ensure Network Watcher is Enabled**

If Network Watcher is not enabled for your region, enable it with:

```bash
bashCopyEditaz network watcher configure --locations <region> --enabled true
```

Example for enabling in `East US`:

```bash
bashCopyEditaz network watcher configure --locations eastus --enabled true
```

#### **2. Create a Packet Capture Session**

Use the following command to start a packet capture:

```bash
bashCopyEditaz network watcher packet-capture create \
  --name MyPacketCapture \
  --resource-group MyResourceGroup \
  --vm MyVMName \
  --storage-account MyStorageAccount \
  --file-path /var/log/mypacketcapture.pcap
```

Replace:

* `MyPacketCapture` → with your preferred packet capture name.
* `MyResourceGroup` → with the resource group where your VM resides.
* `MyVMName` → with the name of your VM.
* `MyStorageAccount` (optional) → Specify if you want to save to Azure Storage.
* `--file-path` → Specify a local path to store the `.pcap` file inside the VM.

#### **3. Apply Packet Capture Filters (Optional)**

To capture only specific traffic, add filters:

```bash
bashCopyEditaz network watcher packet-capture create \
  --name FilteredCapture \
  --resource-group MyResourceGroup \
  --vm MyVMName \
  --file-path /var/log/filtered_capture.pcap \
  --filters "[{'protocol':'TCP', 'remotePort':'443', 'localIpAddress':'10.0.0.4'}]"
```

This command captures only TCP packets sent to **port 443** from IP **10.0.0.4**.

#### **4. List Active Packet Captures**

To see active packet capture sessions:

```bash
bashCopyEditaz network watcher packet-capture list --resource-group MyResourceGroup
```

#### **5. Stop a Packet Capture Session**

To stop a running packet capture:

```bash
bashCopyEditaz network watcher packet-capture stop \
  --name MyPacketCapture \
  --resource-group MyResourceGroup
```

#### **6. Download the Capture File**

If stored in an Azure Storage Account, download it via:

```bash
bashCopyEditaz storage blob download \
  --account-name MyStorageAccount \
  --container-name network-watcher \
  --name MyPacketCapture.cap \
  --file MyPacketCapture.cap
```
