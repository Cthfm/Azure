# VNET Flow Log Schema

## Log format <a href="#log-format" id="log-format"></a>

Virtual network flow logs have the following properties:

### **General Properties**

* **time**: Time in UTC when the event was logged.
* **flowLogVersion**: Version of the flow log.
* **flowLogGUID**: Resource GUID of the FlowLog resource.
* **macAddress**: MAC address of the network interface where the event was captured.
* **category**: Category of the event. This value is always `FlowLogFlowEvent`.
* **flowLogResourceID**: Resource ID of the FlowLog resource.
* **targetResourceID**: Resource ID of the target resource associated with the FlowLog resource.
* **operationName**: Always `FlowLogFlowEvent`.

### **Flow Records Properties**

* **flowRecords**: Collection of flow records.
* **flows**: Collection of flows, which may include multiple entries for access control lists (ACLs).
  * **aclID**: Identifier of the resource evaluating traffic, either a network security group or Virtual Network Manager. If traffic is denied due to encryption, this value is unspecified.

### **Flow Groups Properties**

* **flowGroups**: Collection of flow records at a rule level.
  * **rule**: Name of the rule that allowed or denied the traffic. If traffic is denied due to encryption, this value is unspecified.

### **Flow Tuples Properties**

* **flowTuples**: String containing multiple properties for the flow tuple in a comma-separated format.
  * **Time Stamp**: Time stamp of when the flow occurred, in UNIX epoch format.
  * **Source IP**: Source IP address.
  * **Destination IP**: Destination IP address.
  * **Source port**: Source port.
  * **Destination port**: Destination port.
  * **Protocol**: Layer 4 protocol of the flow, expressed in IANA assigned values.
  * **Flow direction**: Direction of the traffic flow. Valid values are `I` (Inbound) and `O` (Outbound).
  * **Flow state**: State of the flow, with possible values:
    * `B`: Begin (Flow is created, no statistics provided).
    * `C`: Continuing (Ongoing flow, statistics provided at five-minute intervals).
    * `E`: End (Flow terminated, statistics provided).
    * `D`: Deny (Flow is denied).
  * **Flow encryption**: Encryption state of the flow.
  * **Packets sent**: Total number of packets sent from the source to the destination since the last update.
  * **Bytes sent**: Total number of bytes sent from the source to the destination since the last update, including the packet header and payload.
  * **Packets received**: Total number of packets sent from the destination to the source since the last update.
  * **Bytes received**: Total number of bytes sent from the destination to the source since the last update, including the packet header and payload.

