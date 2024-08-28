# NSG Flow Log Schema

## **Schema Reference:**

### **General Properties**

* **time**: Time in UTC when the event was logged.
* **systemId**: System ID of the network security group.
* **category**: Category of the event. This value is always `NetworkSecurityGroupFlowEvent`.
* **resourceid**: Resource ID of the network security group.
* **operationName**: Always `NetworkSecurityGroupFlowEvents`.

### **Flow Properties**

* **properties**: Collection of properties of the flow.
  * **Version**: Version number of the flow log's event schema.
  * **flows**: Collection of flows. This property has multiple entries for different rules.
    * **rule**: Rule for which the flows are listed.
    * **flows**: Collection of flows.
      * **mac**: MAC address of the NIC for the VM where the flow was collected.
      * **flowTuples**: String containing multiple properties for the flow tuple in a comma-separated format.
        * **Time stamp**: Time stamp of when the flow occurred in UNIX epoch format.
        * **Source IP**: Source IP address.
        * **Destination IP**: Destination IP address.
        * **Source port**: Source port.
        * **Destination port**: Destination port.
        * **Protocol**: Protocol of the flow. Valid values are `T` for TCP and `U` for UDP.
        * **Traffic flow**: Direction of the traffic flow. Valid values are `I` for inbound and `O` for outbound.
        * **Traffic decision**: Whether traffic was allowed or denied. Valid values are `A` for allowed and `D` for denied.

### **Flow State Properties (Version 2 Only)**

* **Flow State**: State of the flow, with possible states:
  * `B`: Begin (Flow is created, statistics aren't provided).
  * `C`: Continuing (Ongoing flow, statistics provided at 5-minute intervals).
  * `E`: End (Flow terminated, statistics provided).
* **Packets sent**: Total number of TCP packets sent from source to destination since the last update.
* **Bytes sent**: Total number of TCP packet bytes sent from source to destination since the last update, including the packet header and payload.
* **Packets received**: Total number of TCP packets sent from destination to source since the last update.
* **Bytes received**: Total number of TCP packet bytes sent from destination to source since the last update, including the packet header and payload.

##
