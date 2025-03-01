# Wireshark Cheatsheet

### Overview

The following is a cheat sheet for getting started within Wireshark and how to use it.&#x20;

### **Starting and Stopping Packet Capture**

| **Action**           | **Wireshark Steps**                  | **Shortcut** |
| -------------------- | ------------------------------------ | ------------ |
| **Start Capture**    | Select an interface and click  Start | `Ctrl + E`   |
| **Stop Capture**     | Click Stop                           | `Ctrl + E`   |
| **Save Capture**     | `File → Save As...`                  | `Ctrl + S`   |
| **Open a PCAP File** | `File → Open...`                     | `Ctrl + O`   |
| **Restart Capture**  | `Capture → Restart`                  | `Ctrl + R`   |

**Tip:** Always use **capture filters** before starting a capture to reduce noise.

### **Applying Filters (Capture vs. Display Filters)**

#### **Capture Filters (Set Before Capture)**

**How to Apply:**\
1️. Click **Capture Options (Gear Icon ⚙️)**\
2️. Enter a filter in **Capture Filter** field\
3\. Click **Start**

| **Filter**         | **Purpose**                                      |
| ------------------ | ------------------------------------------------ |
| `port 80`          | Capture **only HTTP** traffic                    |
| `host 192.168.1.1` | Capture **only packets** to/from **192.168.1.1** |
| `tcp`              | Capture **only TCP** packets                     |
| `udp`              | Capture **only UDP** packets                     |
| `icmp`             | Capture **only ICMP (ping)** traffic             |

### **Display Filters (Apply After Capture)**

**How to Apply:**\
1️. Type the filter in **Display Filter Bar**\
2️. Press **Enter**

| **Filter**                                 | **Purpose**                                         |
| ------------------------------------------ | --------------------------------------------------- |
| `ip.addr == 192.168.1.1`                   | Show **all traffic** to/from **192.168.1.1**        |
| `ip.src == 10.0.0.5`                       | Show **only packets originating** from **10.0.0.5** |
| `ip.dst == 8.8.8.8`                        | Show **only packets going** to **8.8.8.8**          |
| `tcp.port == 443`                          | Show **only HTTPS traffic**                         |
| `dns`                                      | Show **only DNS requests & responses**              |
| `http.request`                             | Show **only HTTP requests**                         |
| `tls.handshake.type == 1`                  | Show **only TLS Client Hello packets**              |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Detect **SYN scans (port scanning)**                |
| `frame contains "password"`                | Find packets **containing "password"**              |

**Tip:** Use `&&` (AND), `||` (OR), and `!` (NOT) to combine filters.\
Example: `tcp && !port 22` (Show **only TCP**, but **exclude SSH traffic**).

### **Useful Wireshark Features for Analysis**

#### **Follow Network Streams (View Full Conversations)**

**Steps:**\
1️. Right-click a packet → `Follow` → `TCP Stream` / `UDP Stream`\
2️. View full conversation between source & destination

#### **Extract Files from Traffic (HTTP, SMB, FTP, etc.)**

**Steps:**\
1️. `File` → `Export Objects`\
2️. Choose protocol (HTTP, SMB, FTP, etc.)\
3️. Select files & click Save

#### **Analyze Protocol Hierarchy**

**How to Use:**\
1️.`Statistics` → `Protocol Hierarchy`\
2️. View percentage of traffic per protocol (TCP, HTTP, DNS, etc.)

#### **Visualize Packet Flow**

**How to Use:**\
1️. `Statistics` → `Flow Graph`\
2️. See how packets flow between devices (useful for debugging)

#### **Check for Network Errors (Expert Info)**

**How to Use:**\
1️. `Analyze` → `Expert Information`\
2️. View warnings, errors, and dropped packets

#### **Identify Long Connections (IO Graphs)**

**How to Use:**\
1️. `Statistics` → `I/O Graphs`\
2️. Identify sudden traffic spikes, DoS attacks, or exfiltration

### **Packet Inspection & Troubleshooting**

| **Issue**                      | **Feature to Use**                      | **Shortcut** |
| ------------------------------ | --------------------------------------- | ------------ |
| **Investigate Latency Issues** | `Analyze → Expert Info`                 | -            |
| **Analyze TCP Handshakes**     | `Statistics → Flow Graph`               | -            |
| **Find HTTP Requests**         | `http.request` filter                   | -            |
| **Detect DNS Exfiltration**    | `dns.qry.name contains "malicious.com"` | -            |
| **Analyze TLS Traffic**        | `tls.handshake.type == 1`               | -            |

Tip: Use Wireshark profiles to create custom settings for different scenarios (e.g., forensics, troubleshooting, red teaming).

### **Wireshark Keyboard Shortcuts for Speed**

| **Shortcut**       | **Action**                                |
| ------------------ | ----------------------------------------- |
| `Ctrl + E`         | **Start/Stop Capture**                    |
| `Ctrl + S`         | **Save Capture**                          |
| `Ctrl + O`         | **Open a PCAP file**                      |
| `Ctrl + F`         | **Find packets by string, hex, etc.**     |
| `Ctrl + M`         | **Mark a packet**                         |
| `Shift + Ctrl + N` | **Go to next packet in conversation**     |
| `Shift + Ctrl + B` | **Go to previous packet in conversation** |
| `Ctrl + T`         | **Set Time Reference (Latency Analysis)** |
| `Shift + ← / →`    | **Expand/Collapse packet details**        |
