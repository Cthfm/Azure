# TShark Cheatsheet

## Overview:

Wireshark provides a command line option called TShark. For those that are familiar with Tcpdump this solution is similar but uses Wireshark related syntax.&#x20;

### **1️. Basic Capture Commands**

| Command                | Description                                       |
| ---------------------- | ------------------------------------------------- |
| tshark                 | Start capturing packets on the default interface. |
| tshark -i eth0         | Capture packets on a specific interface (`eth0`). |
| tshark -D              | List all available network interfaces.            |
| tshark -c 10           | Capture only 10 packets and then stop.            |
| tshark -w capture.pcap | Save packets to a .pcap file.                     |
| tshark -r capture.pcap | Read packets from a saved .pcap file.             |

### **2️. Display Packet Details**

| Command                              | Description                                           |
| ------------------------------------ | ----------------------------------------------------- |
| tshark -V                            | Show verbose output with full packet details.         |
| tshark -x                            | Show packet data in hex and ASCII.                    |
| tshark -O http                       | Show only HTTP packet details.                        |
| tshark -n                            | Disable hostname and port resolution (faster output). |
| tshark -T fields -e ip.src -e ip.dst | Display only source and destination IPs.              |
| tshark -T json                       | Output packets in JSON format.                        |

### **3️. Filtering Packets (Capture Filters)**

| Command                             | Description                                    |
| ----------------------------------- | ---------------------------------------------- |
| tshark -i eth0 port 80              | Capture only HTTP traffic.                     |
| tshark -i eth0 host 192.168.1.1     | Capture packets to/from a specific host.       |
| tshark -i eth0 net 192.168.1.0/24   | Capture packets from a subnet.                 |
| tshark -i eth0 src host 192.168.1.1 | Capture packets from a source IP.              |
| tshark -i eth0 dst port 443         | Capture packets destined for port 443 (HTTPS). |

### **4️. Filtering Packets (Display Filters)**

| Filter                             | Description                      |
| ---------------------------------- | -------------------------------- |
| tshark -Y "ip.addr == 192.168.1.1" | Show all packets to/from an IP.  |
| tshark -Y "tcp.port == 80"         | Show only HTTP traffic.          |
| tshark -Y "udp"                    | Show only UDP traffic.           |
| tshark -Y "icmp"                   | Show only ICMP (ping) packets.   |
| tshark -Y "dns"                    | Show only DNS traffic.           |
| tshark -Y "http.request"           | Show only HTTP requests.         |
| tshark -Y "ssl.handshake"          | Show only SSL handshake packets. |
| tshark -Y "tcp.flags.syn == 1"     | Show only TCP SYN packets.       |

### **5️. Extracting Specific Fields**

| Command                                            | Description                           |
| -------------------------------------------------- | ------------------------------------- |
| tshark -T fields -e ip.src -e ip.dst               | Show only source and destination IPs. |
| tshark -T fields -e http.host                      | Extract HTTP hostnames.               |
| tshark -T fields -e dns.qry.name                   | Extract DNS queries.                  |
| tshark -T fields -e frame.time -e ip.src -e ip.dst | Show timestamps with IP addresses.    |
| tshark -T fields -e tls.handshake.ciphersuite      | Show TLS cipher suites.               |

***

### **6️. Advanced Packet Analysis**

| Command                     | Description                                         |
| --------------------------- | --------------------------------------------------- |
| tshark -Y "tcp.stream eq 5" | Show packets for a specific TCP stream.             |
| tshark -z io,stat,1         | Show packet statistics per second.                  |
| tshark -z conv,tcp          | Show TCP conversations.                             |
| tshark -z endpoints,ip      | List all unique IP addresses seen in traffic.       |
| tshark -q -z expert         | Show expert info (protocol errors, warnings, etc.). |

***

### **7️. Extracting and Analyzing Data**

| Command                                                            | Description                                      |
| ------------------------------------------------------------------ | ------------------------------------------------ |
| tshark -r capture.pcap -Y "http.request" -T fields -e http.host    | Extract HTTP hostnames.                          |
| tshark -r capture.pcap -Y "dns" -T fields -e dns.qry.name          | Extract all DNS queries.                         |
| tshark -r capture.pcap -Y "tcp.port == 443" -w https\_traffic.pcap | Save only HTTPS traffic to a new file.           |
| tshark -r capture.pcap -Y "tcp.analysis.retransmission"            | Show TCP retransmissions.                        |
| tshark -r capture.pcap -Y "ip.geoip.country == 'United States'"    | Filter traffic by country (if GeoIP is enabled). |

***

### **8️. Wireshark-Compatible Filters**

After capturing packets with tshark, you can analyze them in **Wireshark** using these filters:

| Wireshark Filter                   | Description                             |
| ---------------------------------- | --------------------------------------- |
| http                               | Show only HTTP traffic.                 |
| tcp.flags.syn == 1                 | Show only SYN packets.                  |
| ip.addr == 192.168.1.1             | Show all traffic to/from a specific IP. |
| dns.qry.name contains "google.com" | Show only DNS queries for "google.com". |
| ssl.handshake.type == 1            | Show only SSL Client Hello messages.    |

***

### **Pro Tips**

1. **Run tshark as root for full packet capture:**

```bash
sudo tshark -i eth0
```

2. &#x20;**Stop capture after N packets**:

```bash
tshark -c 100 -w sample.pcap
```

3. **Analyze a specific protocol in a PCAP file:**

```bash
tshark -r sample.pcap -Y "icmp"
```

4. &#x20;**Extract unique IP addresses from a PCAP**:

```bash
tshark -r sample.pcap -T fields -e ip.src -e ip.dst | sort | uniq
```
