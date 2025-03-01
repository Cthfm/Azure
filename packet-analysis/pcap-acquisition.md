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
