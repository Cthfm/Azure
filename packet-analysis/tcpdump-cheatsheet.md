# TCPDUMP Cheatsheet

## Overview:

In certain environments you may or may not have access to tshark or wireshark. Tcpdump is generally available on many different distributions. This assumes the administrator allows it. Here is a cheatsheet to get started.&#x20;

### **1️. Basic Capture Commands**

| Command                 | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| tcpdump                 | Start capturing packets on the default interface.       |
| tcpdump -i eth0         | Capture packets on a specific interface (e.g., `eth0`). |
| tcpdump -D              | List all available network interfaces.                  |
| tcpdump -c 10           | Capture only 10 packets and then stop.                  |
| tcpdump -w capture.pcap | Save packets to a file for later analysis.              |
| tcpdump -r capture.pcap | Read packets from a previously saved file.              |

### **2️. Filtering Traffic**

| Command                      | Description                                              |
| ---------------------------- | -------------------------------------------------------- |
| tcpdump host 192.168.1.1     | Capture traffic to/from a specific host.                 |
| tcpdump src host 192.168.1.1 | Capture packets only from a source IP.                   |
| tcpdump dst host 192.168.1.1 | Capture packets only to a destination IP.                |
| tcpdump net 192.168.1.0/24   | Capture traffic from a specific subnet.                  |
| tcpdump port 80              | Capture packets on a specific port (e.g., HTTP traffic). |
| tcpdump src port 443         | Capture packets from a specific source port.             |
| tcpdump dst port 53          | Capture packets to a specific destination port.          |

### **3. Protocol-Specific Capture**

| Command             | Description                            |
| ------------------- | -------------------------------------- |
| tcpdump tcp         | Capture only TCP traffic.              |
| tcpdump udp         | Capture only UDP traffic.              |
| tcpdump icmp        | Capture only ICMP (ping) traffic.      |
| tcpdump arp         | Capture only ARP packets.              |
| tcpdump port not 22 | Capture everything except SSH traffic. |

### **4️. Display Packet Details**

| Command       | Description                                               |
| ------------- | --------------------------------------------------------- |
| tcpdump -X    | Show packet contents in hex and ASCII.                    |
| tcpdump -XX   | Show full packet details including link-layer headers.    |
| tcpdump -A    | Show ASCII output (useful for inspecting HTTP traffic).   |
| tcpdump -tttt | Show human-readable timestamps.                           |
| tcpdump -n    | Do not resolve IP addresses to hostnames (faster output). |
| tcpdump -nn   | Do not resolve hostnames or port numbers (pure numeric).  |

### **5️. Advanced Filters**

| Command                                  | Description                               |
| ---------------------------------------- | ----------------------------------------- |
| tcpdump 'tcp\[13] & 2 != 0'              | Capture only SYN packets (TCP handshake). |
| tcpdump 'tcp\[13] & 16 != 0'             | Capture only ACK packets.                 |
| tcpdump 'tcp\[tcpflags] & tcp-push != 0' | Capture only PUSH packets.                |
| tcpdump 'icmp\[icmptype] = icmp-echo'    | Capture only ICMP echo requests (ping).   |
| tcpdump 'greater 1000'                   | Capture packets larger than 1000 bytes.   |

### **6️. Combine Multiple Filters**

| Command                                                   | Description                                   |
| --------------------------------------------------------- | --------------------------------------------- |
| tcpdump src host 192.168.1.1 and dst port 80              | Capture packets from a source IP to port 80.  |
| tcpdump '(src net 192.168.1.0/24) and (dst port 443)'     | Capture HTTPS traffic from a specific subnet. |
| tcpdump 'tcp port 80 and (tcp\[tcpflags] & tcp-syn != 0)' | Capture only HTTP SYN packets.                |

### **7️. Capture and Analyze Specific Traffic**

| Task                                              | Command                              |
| ------------------------------------------------- | ------------------------------------ |
| Capture all HTTP traffic                          | tcpdump -i eth0 port 80 -A           |
| Capture all DNS queries                           | tcpdump -i eth0 port 53 -nn          |
| Capture SSH brute force attempts                  | tcpdump -i eth0 src port 22          |
| Capture packets larger than 1KB                   | tcpdump greater 1024                 |
| Capture traffic related to a specific MAC address | tcpdump ether host 00:11:22:33:44:55 |

### **8️. Save and Read Packets**

| Command                       | Description                                 |
| ----------------------------- | ------------------------------------------- |
| tcpdump -w output.pcap        | Save packets to a file.                     |
| tcpdump -r output.pcap        | Read packets from a saved file.             |
| tcpdump -r output.pcap -nn -X | Read packets and display detailed contents. |

### **9️. Useful Wireshark Filters**

After capturing packets with tcpdump, open the .pcap file in Wireshark and apply these filters:

| Wireshark Filter         | Description                             |
| ------------------------ | --------------------------------------- |
| `http`                   | Show only HTTP traffic.                 |
| `tcp.flags.syn == 1`     | Show only SYN packets.                  |
| `ip.addr == 192.168.1.1` | Show all traffic to/from a specific IP. |
| `dns`                    | Show only DNS queries.                  |
| `ssl`                    | Show only SSL/TLS traffic.              |

***

### **Pro Tips**

1\. **Run tcpdump as root for full packet capture:**

```bash
sudo tcpdump -i eth0
```

2\. **Stop capture after N packets**:

```bash
tcpdump -c 100 -w sample.pcap
```

3\. **Analyze a specific protocol** in a PCAP file:

```bash
tcpdump -r sample.pcap icmp
```

4\. **Find out which process is generating network traffic**:

```bash
sudo netstat -anp | grep :80
```
