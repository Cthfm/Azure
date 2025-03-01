# Protocol Analysis Basics

### **📡 1. TCP (Transmission Control Protocol)**

🔹 **Purpose:** Provides reliable, ordered, and error-checked communication between applications.\
🔹 **Common Ports:** 80 (HTTP), 443 (HTTPS), 22 (SSH), 25 (SMTP), 3389 (RDP)

#### **🔍 How TCP Works**

1️⃣ **SYN** → Client requests connection (sends `SYN` packet).\
2️⃣ **SYN-ACK** → Server acknowledges request (sends `SYN-ACK`).\
3️⃣ **ACK** → Client confirms (sends `ACK`).

✅ **This process is called the "Three-Way Handshake."**

#### **🔍 Key Fields in Wireshark**

| **Field**                              | **Description**                                     |
| -------------------------------------- | --------------------------------------------------- |
| `Sequence Number (Seq)`                | Tracks packet order in a connection.                |
| `Acknowledgment Number (Ack)`          | Ensures packets were received.                      |
| `Window Size (Win Size)`               | Controls data flow to prevent overload.             |
| `Flags (SYN, ACK, FIN, RST, PSH, URG)` | Show connection state (handshake, closing, errors). |

#### **🔎 Wireshark Filters**

| **Filter**           | **Description**                         |
| -------------------- | --------------------------------------- |
| `tcp`                | Show all TCP packets.                   |
| `tcp.flags.syn == 1` | Show connection requests (SYN packets). |
| `tcp.flags.fin == 1` | Show connection closure attempts.       |

***

### **🌍 2. HTTP (Hypertext Transfer Protocol)**

🔹 **Purpose:** Transfers web pages between browsers and web servers.\
🔹 **Common Ports:** 80

#### **🔍 How HTTP Works**

1️⃣ **Browser sends a request (HTTP Request)**

* Example: `GET /index.html` (requests a webpage).\
  2️⃣ **Server sends a response (HTTP Response)**
* Example: `HTTP/1.1 200 OK` (returns the requested page).

#### **🔍 Key Fields in Wireshark**

| **Field**                         | **Description**                               |
| --------------------------------- | --------------------------------------------- |
| `Method (GET, POST, PUT, DELETE)` | Type of request being made.                   |
| `Status Code (200, 404, 500)`     | Response status (OK, Not Found, Error).       |
| `Host`                            | Website being requested.                      |
| `User-Agent`                      | Identifies browser/device making the request. |

#### **🔎 Wireshark Filters**

| **Filter**                     | **Description**                  |
| ------------------------------ | -------------------------------- |
| `http`                         | Show all HTTP traffic.           |
| `http.request.method == "GET"` | Show only GET requests.          |
| `http.response.code == 404`    | Show only "Not Found" responses. |

***

### **🔐 3. HTTPS (HTTP Secure - Encrypted Web Traffic)**

🔹 **Purpose:** Secure version of HTTP that encrypts communication.\
🔹 **Common Ports:** 443

#### **🔍 How HTTPS Works**

1️⃣ **Client sends "Client Hello"** → Lists supported encryption methods.\
2️⃣ **Server responds with "Server Hello"** → Chooses encryption type.\
3️⃣ **Key Exchange** → Client and server establish a secure connection.\
4️⃣ **Encrypted Communication** → Data is exchanged securely.

#### **🔍 Key Fields in Wireshark**

| **Field**      | **Description**                       |
| -------------- | ------------------------------------- |
| `Client Hello` | Starts secure connection negotiation. |
| `Server Hello` | Server chooses encryption settings.   |
| `Certificate`  | Proves website's identity.            |

#### **🔎 Wireshark Filters**

| **Filter**                | **Description**                  |
| ------------------------- | -------------------------------- |
| `tls`                     | Show all TLS (HTTPS) traffic.    |
| `tls.handshake.type == 1` | Show Client Hello messages.      |
| `tls.record.version`      | Show specific TLS versions used. |

***

### **📨 4. DNS (Domain Name System)**

🔹 **Purpose:** Translates domain names (e.g., google.com) into IP addresses.\
🔹 **Common Ports:** 53

#### **🔍 How DNS Works**

1️⃣ **Client asks "What is the IP address for google.com?"**\
2️⃣ **DNS Server responds with "It is 142.250.185.206."**\
3️⃣ **Client connects to that IP to access the website.**

#### **🔍 Key Fields in Wireshark**

| **Field**                         | **Description**                    |
| --------------------------------- | ---------------------------------- |
| `Query Name`                      | Domain name being looked up.       |
| `Response Address`                | IP address returned by DNS server. |
| `Query Type (A, AAAA, MX, CNAME)` | Type of record requested.          |

#### **🔎 Wireshark Filters**

| **Filter**                      | **Description**                     |
| ------------------------------- | ----------------------------------- |
| `dns`                           | Show all DNS traffic.               |
| `dns.qry.name == "example.com"` | Show queries for a specific domain. |

***

### **📞 5. VoIP (SIP & RTP - Voice Over IP)**

🔹 **Purpose:** Used for internet-based voice calls.\
🔹 **Common Ports:** 5060 (SIP), 16384-32767 (RTP)

#### **🔍 How VoIP Works**

1️⃣ **SIP (Session Initiation Protocol) handles call setup.**

* Example: "INVITE" message starts a call.\
  2️⃣ **RTP (Real-Time Protocol) sends audio/video.**

#### **🔍 Key Fields in Wireshark**

| **Field** | **Description**           |
| --------- | ------------------------- |
| `INVITE`  | Starts a call session.    |
| `200 OK`  | Call accepted.            |
| `RTP`     | Transmits voice or video. |

#### **🔎 Wireshark Filters**

| **Filter** | **Description**             |
| ---------- | --------------------------- |
| `sip`      | Show all SIP traffic.       |
| `rtp`      | Show all RTP voice packets. |

***

### **📡 6. ARP (Address Resolution Protocol)**

🔹 **Purpose:** Resolves IP addresses to MAC addresses.\
🔹 **Common Use:** Allows devices to communicate over local networks.

#### **🔍 How ARP Works**

1️⃣ **Device asks "Who has IP 192.168.1.1?"**\
2️⃣ **Owner replies "That’s me! My MAC address is AA:BB:CC:DD:EE:FF."**

#### **🔍 Key Fields in Wireshark**

| **Field**                         | **Description**                               |
| --------------------------------- | --------------------------------------------- |
| `Opcode (1 = Request, 2 = Reply)` | Shows if the packet is a request or response. |
| `Sender IP`                       | Device making the request.                    |
| `Sender MAC`                      | MAC address of requesting device.             |

#### **🔎 Wireshark Filters**

| **Filter**        | **Description**         |
| ----------------- | ----------------------- |
| `arp`             | Show all ARP packets.   |
| `arp.opcode == 1` | Show only ARP requests. |

***

### **📦 7. DHCP (Dynamic Host Configuration Protocol)**

🔹 **Purpose:** Assigns IP addresses to devices on a network.\
🔹 **Common Ports:** 67 (server), 68 (client)

#### **🔍 How DHCP Works**

1️⃣ **Client broadcasts "I need an IP address!"**\
2️⃣ **Server responds "Here is an IP address you can use."**

#### **🔍 Key Fields in Wireshark**

| **Field**  | **Description**                   |
| ---------- | --------------------------------- |
| `Discover` | Client request for an IP address. |
| `Offer`    | Server offers an IP address.      |
| `Request`  | Client accepts the IP address.    |
| `ACK`      | Server confirms the lease.        |

#### **🔎 Wireshark Filters**

| **Filter** | **Description**        |
| ---------- | ---------------------- |
| `dhcp`     | Show all DHCP traffic. |
