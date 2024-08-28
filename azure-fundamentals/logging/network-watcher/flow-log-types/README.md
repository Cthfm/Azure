# Flow Log Types

Azure Network Watcher provides two types of flow logs: Network Security Group (NSG) Flow Logs and Virtual Network (VNet) Flow Logs.&#x20;

## NSG Flow Logs

1. **Purpose**:
   * Capture information about ingress and egress IP traffic through Network Security Groups (NSGs).
2. **Details Captured**:
   * Records include source and destination IP addresses, source and destination ports, protocol, traffic flow action (allowed or denied), and traffic flow direction (inbound or outbound).
3. **Use Cases**:
   * Monitor and analyze network security policies.
   * Identify unauthorized access attempts or misconfigurations in NSG rules.
   * Troubleshoot connectivity issues related to NSG configurations.
4. **Storage**:
   * Logs are stored in an Azure Storage account, making it easy to access and analyze using tools like Azure Log Analytics.

## VNet Flow Logs

1. **Purpose**:
   * Capture detailed information about traffic flows within a Virtual Network (VNet), including traffic not passing through NSGs.
2. **Details Captured**:
   * More granular data compared to NSG Flow Logs, including deeper insights into the network traffic between VMs within the same VNet or across VNets.
3. **Use Cases**:
   * Gain comprehensive visibility into network traffic patterns within and between VNets.
   * Detect and analyze internal network threats and anomalies that do not interact with NSGs.
   * Optimize network performance by understanding detailed traffic flows.
4. **Storage**:
   * Similar to NSG Flow Logs, VNet Flow Logs are stored in an Azure Storage account and can be analyzed using various Azure tools.

## Key Differences

* **Scope**: NSG Flow Logs focus on traffic controlled by NSGs, capturing data on traffic allowed or denied by security rules. VNet Flow Logs provide a broader view of traffic within and between VNets, not limited to NSG interactions.
* **Details**: VNet Flow Logs offer more detailed traffic information, suitable for comprehensive network traffic analysis, while NSG Flow Logs are more focused on security rule enforcement and network security monitoring.
