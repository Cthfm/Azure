# Packet Capture

## What is Packet Capture?

Packet capture in Azure Network Watcher allows you to capture network traffic to and from virtual machines (VMs) for further analysis. This feature is essential for diagnosing network issues, analyzing traffic patterns, and detecting suspicious activities.

## Key Features

1. **Capture on Demand**:
   * Initiate packet capture in real-time whenever required.
   * Define filters to capture specific types of traffic (e.g., based on IP address, port, protocol).
2. **Scheduled Captures**:
   * Schedule packet captures to run at specific times or intervals.
   * Useful for continuous monitoring or capturing traffic during anticipated events.
3. **Granular Control**:
   * Apply capture filters to control what data is captured, reducing the volume of data to analyze.
   * Capture based on criteria such as source IP, destination IP, source port, destination port, and protocol.
4. **Storage Options**:
   * Captured packets can be stored in an Azure Storage account for easy access and long-term retention.
   * Download captured files in .pcap format for analysis using tools like Wireshark.
5. **Integration with Other Azure Services**:
   * Easily integrates with other Azure services, such as Azure Security Center, for enhanced security monitoring and analysis.
   * Use captured data in conjunction with Azure Log Analytics for deeper insights.

### Microsoft Documentation

{% embed url="https://learn.microsoft.com/en-us/azure/network-watcher/packet-capture-overview" %}
