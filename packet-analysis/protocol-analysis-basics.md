# Protocol Analysis Basics

### **Overview:**

The following is a list of protocols that security analysts and cyber defenders will see while responding to security alerts and doing traffic analysis. This guide gives you a quick understanding of the protocol. For further knowledge it is recommended to review the associated RFC documentation. A mapping of the protocol RFC pages is provided within this section of the CTHFM.

### **1. TCP (Transmission Control Protocol)**

**Purpose:** Provides reliable, ordered, and error-checked communication between applications.\
**Common Ports:** 80 (HTTP), 443 (HTTPS), 22 (SSH), 25 (SMTP), 3389 (RDP)

#### **How TCP Works**

1️. **SYN** → Client requests connection (sends `SYN` packet).\
2️. **SYN-ACK** → Server acknowledges request (sends `SYN-ACK`).\
3️. **ACK** → Client confirms (sends `ACK`).

{% hint style="info" %}
This process is called the "Three-Way Handshake."
{% endhint %}

#### **Key Fields in Wireshark**

| **Field**                            | **Description**                                     |
| ------------------------------------ | --------------------------------------------------- |
| Sequence Number (Seq)                | Tracks packet order in a connection.                |
| Acknowledgment Number (Ack)          | Ensures packets were received.                      |
| Window Size (Win Size)               | Controls data flow to prevent overload.             |
| Flags (SYN, ACK, FIN, RST, PSH, URG) | Show connection state (handshake, closing, errors). |

#### **Wireshark Filters**

| **Filter**         | **Description**                         |
| ------------------ | --------------------------------------- |
| tcp                | Show all TCP packets.                   |
| tcp.flags.syn == 1 | Show connection requests (SYN packets). |
| tcp.flags.fin == 1 | Show connection closure attempts.       |

***

### **2. HTTP (Hypertext Transfer Protocol)**

**Purpose:** Transfers web pages between browsers and web servers.\
&#x20;**Common Ports:** 80

#### **How HTTP Works**

1️. **Browser sends a request (HTTP Request)**

&#x20;    Example: `GET /index.html` (requests a webpage).\


2.  **Server sends a response (HTTP Response)**



    Example: `HTTP/1.1 200 OK` (returns the requested page).

#### **Key Fields in Wireshark**

| **Field**                       | **Description**                               |
| ------------------------------- | --------------------------------------------- |
| Method (GET, POST, PUT, DELETE) | Type of request being made.                   |
| Status Code (200, 404, 500)     | Response status (OK, Not Found, Error).       |
| Host                            | Website being requested.                      |
| User-Agent                      | Identifies browser/device making the request. |

#### **Wireshark Filters**

| **Filter**                   | **Description**                  |
| ---------------------------- | -------------------------------- |
| http                         | Show all HTTP traffic.           |
| http.request.method == "GET" | Show only GET requests.          |
| http.response.code == 404    | Show only "Not Found" responses. |

### **3. HTTPS (HTTP Secure - Encrypted Web Traffic)**

**Purpose:** Secure version of HTTP that encrypts communication.\
**Port:** 443

#### **How HTTPS Works**

1️. **Client sends "Client Hello"** → Lists supported encryption methods.\
2️. **Server responds with "Server Hello"** → Chooses encryption type.\
3️. **Key Exchange** → Client and server establish a secure connection.\
4️. **Encrypted Communication** → Data is exchanged securely.

#### **Key Fields in Wireshark**

| **Field**    | **Description**                       |
| ------------ | ------------------------------------- |
| Client Hello | Starts secure connection negotiation. |
| Server Hello | Server chooses encryption settings.   |
| Certificate  | Proves website's identity.            |

#### **Wireshark Filters**

| **Filter**              | **Description**                  |
| ----------------------- | -------------------------------- |
| tls                     | Show all TLS (HTTPS) traffic.    |
| tls.handshake.type == 1 | Show Client Hello messages.      |
| tls.record.version      | Show specific TLS versions used. |

***

### **4. DNS (Domain Name System)**

**Purpose:** Translates domain names (e.g., google.com) into IP addresses.\
**Port:** 53

#### **How DNS Works**

1️. **Client asks "What is the IP address for google.com?"**\
2️. **DNS Server responds with "It is 142.250.185.206."**\
3️. **Client connects to that IP to access the website.**

#### **Key Fields in Wireshark**

| **Field**                       | **Description**                    |
| ------------------------------- | ---------------------------------- |
| Query Name                      | Domain name being looked up.       |
| Response Address                | IP address returned by DNS server. |
| Query Type (A, AAAA, MX, CNAME) | Type of record requested.          |

#### **Wireshark Filters**

| **Filter**                    | **Description**                     |
| ----------------------------- | ----------------------------------- |
| dns                           | Show all DNS traffic.               |
| dns.qry.name == "example.com" | Show queries for a specific domain. |

***

### **5. VoIP (SIP & RTP - Voice Over IP)**

**Purpose:** Used for internet-based voice calls.\
**Common Ports:** 5060 (SIP), 16384-32767 (RTP)

#### **How VoIP Works**

1️. **SIP (Session Initiation Protocol) handles call setup.**

* Example: "INVITE" message starts a call.

&#x20;2\. **RTP (Real-Time Protocol) sends audio/video.**

#### **Key Fields in Wireshark**

| **Field** | **Description**           |
| --------- | ------------------------- |
| INVITE    | Starts a call session.    |
| 200 OK    | Call accepted.            |
| RTP       | Transmits voice or video. |

#### **Wireshark Filters**

| **Filter** | **Description**             |
| ---------- | --------------------------- |
| sip        | Show all SIP traffic.       |
| rtp        | Show all RTP voice packets. |

***

### **6. ARP (Address Resolution Protocol)**

**Purpose:** Resolves IP addresses to MAC addresses.\
**Common Use:** Allows devices to communicate over local networks.

#### **How ARP Works**

1️. **Device asks "Who has IP 192.168.1.1?"**\
2️. **Owner replies "That’s me! My MAC address is AA:BB:CC:DD:EE:FF."**

#### **Key Fields in Wireshark**

| **Field**                       | **Description**                               |
| ------------------------------- | --------------------------------------------- |
| Opcode (1 = Request, 2 = Reply) | Shows if the packet is a request or response. |
| Sender IP                       | Device making the request.                    |
| Sender MAC                      | MAC address of requesting device.             |

#### **Wireshark Filters**

| **Filter**      | **Description**         |
| --------------- | ----------------------- |
| `arp`           | Show all ARP packets.   |
| arp.opcode == 1 | Show only ARP requests. |

***

### **7. DHCP (Dynamic Host Configuration Protocol)**

**Purpose:** Assigns IP addresses to devices on a network.\
**Common Ports:** 67 (server), 68 (client)

#### **How DHCP Works**

1️. **Client broadcasts "I need an IP address!"**\
2️. **Server responds, "Here is an IP address you can use."**

#### **Key Fields in Wireshark**

| **Field** | **Description**                   |
| --------- | --------------------------------- |
| Discover  | Client request for an IP address. |
| Offer     | Server offers an IP address.      |
| Request   | Client accepts the IP address.    |
| ACK       | Server confirms the lease.        |

#### **Wireshark Filters**

| **Filter** | **Description**        |
| ---------- | ---------------------- |
| dhcp       | Show all DHCP traffic. |

### **8. NTP Basics**

**Common Port:** UDP 123\
**Primary Function:** Synchronizes system clocks with an NTP server

#### **How NTP Works**

1️. Client sends request → "What time is it?"\
2️. Server responds → "The time is 12:00:00 UTC"\
3️. Client adjusts its clock based on the response

**NTP adjusts for network delay** to ensure accuracy.\
**Stratum Levels**: Defines accuracy relative to the primary time source.

* **Stratum 0**: High-precision clocks (GPS, atomic clocks)
* **Stratum 1**: Directly connected to Stratum 0 (e.g., time servers)
* **Stratum 2+**: Synchronizes from higher-stratum servers

#### **Key NTP Packet Fields in Wireshark**

| **Field**           | **Description**                                                                         |
| ------------------- | --------------------------------------------------------------------------------------- |
| Leap Indicator (LI) | Shows clock synchronization status (0 = accurate, 3 = unsynchronized).                  |
| Version Number      | NTP version used (common: v3, v4).                                                      |
| Mode                | Defines packet type (3 = Client, 4 = Server).                                           |
| Stratum             | Server's accuracy level (0 = atomic clock, 1 = primary server, 2+ = secondary servers). |
| Transmit Timestamp  | The exact time the server sends the response.                                           |
| Originate Timestamp | The time the client sent the request.                                                   |
| Reference Timestamp | The last time the server was updated.                                                   |
| Root Delay          | Round-trip delay to the reference clock.                                                |
| Root Dispersion     | Maximum expected clock error.                                                           |

***

#### **Wireshark Filters for NTP**

| **Filter**                 | **Description**                                 |
| -------------------------- | ----------------------------------------------- |
| ntp                        | Show all NTP traffic.                           |
| udp.port == 123            | Filter NTP traffic based on port.               |
| ntp.mode == 3              | Show only client requests.                      |
| ntp.mode == 4              | Show only server responses.                     |
| ntp.stratum == 1           | Show packets from primary NTP server&#x73;**.** |
| ntp.leap != 0              | Find unsynchronized clocks.                     |
| ntp.root\_delay > 100      | Identify servers with high delay.               |
| ntp.root\_dispersion > 100 | Show servers with inconsistent time sources.    |

#### **NTP Communication in Wireshark**

1️. **Find an NTP request** (`ntp.mode == 3`)\
2️. **Locate the corresponding response** (`ntp.mode == 4`)\
3️. **Compare timestamps**:

* `Originate Timestamp` (Client sends request)
* `Receive Timestamp` (Server receives request)
* `Transmit Timestamp` (Server sends response)
* `Destination Timestamp` (Client receives response)

The difference between Originate and Destination timestamps shows round-trip delay.\
&#x20;If Root Dispersion is high, the server’s time may not be reliable.

#### **Understanding NTP Synchronization**

| **Scenario**                     | **Possible Cause**        | **Filter to Use**                   |
| -------------------------------- | ------------------------- | ----------------------------------- |
| Clock drift (system time is off) | Server is unreliable      | `ntp.stratum > 2`                   |
| NTP server unreachable           | Firewall blocking UDP 123 | `ntp && ip.dst == <server IP>`      |
| High time delay                  | Network congestion        | `ntp.root_delay > 100`              |
| Incorrect timestamps             | Spoofed/malicious server  | `ntp.stratum == 0 && ntp.leap == 3` |

### **9. SMB (Server Message Block)**

**Purpose:** SMB (Server Message Block) is a protocol used for file sharing, printer access, and network communication between Windows machines. It allows users to read, write, and execute files on remote systems over a network.

#### **SMB Protocol Basics**

**Common Ports:** 445 (Direct SMB), 137-139 (NetBIOS for older SMB versions)\
**Protocol Type:** TCP\
**Common Uses:**

* File & printer sharing
* Network authentication (Active Directory)
* Remote file execution (Windows shares)

#### **Key SMB Versions**

| **SMB Version**   | **Description**                                  | **Wireshark Filter** |
| ----------------- | ------------------------------------------------ | -------------------- |
| **SMBv1** (1980s) | Oldest, less secure (disabled in modern Windows) | `smb`                |
| **SMBv2** (2006)  | Improved security and performance                | `smb2`               |
| **SMBv3** (2012)  | Supports encryption & compression                | `smb2`               |

#### **Check SMB version using Wireshark:** 1️. Open an SMB packet 2️. Look at `Negotiate Protocol Request` 3️. Check the `Dialect` field (e.g., **"2.1" for SMBv2.1**)

#### **How SMB Works**

1️. **Client sends "Negotiate Protocol Request"** → Requests SMB version.\
2️. **Server replies with "Negotiate Protocol Response"** → Confirms SMB version.\
3️. **Client sends "Session Setup Request"** → Attempts authentication.\
4️. **Server replies with "Session Setup Response"** → Approves or denies access.\
5️. **Client requests a file/share** (`Tree Connect Request`).\
6️. **File operations occur** (`Create, Read, Write, Close`).

#### **Key SMB Packet Fields in Wireshark**

| **Field**                    | **Description**                        | **Use Case**                  |
| ---------------------------- | -------------------------------------- | ----------------------------- |
| Negotiate Protocol Request   | Initial handshake, selects SMB version | Identify SMBv1 vs. SMBv2+     |
| Session Setup Request        | Contains authentication credentials    | Check authentication attempts |
| Tree Connect Request         | Requests access to a shared resource   | See which shares are accessed |
| NT Create AndX Request       | Opens a file or directory              | Find files being accessed     |
| Read Request / Write Request | Reads/writes data from/to a file       | Identify large file transfers |
| Close Request                | Closes a file                          | Find session terminations     |
| Logoff Request               | Ends SMB session                       | Detect session closures       |

***

#### **Wireshark Filters for SMB**

| **Filter**                     | **Description**                       |
| ------------------------------ | ------------------------------------- |
| smb                            | Show all SMB traffic (includes SMBv1) |
| smb2                           | Show only SMBv2/3 traffic             |
| tcp.port == 445                | Capture direct SMB traffic            |
| smb2.cmd == 0x03               | Show only SMB file reads              |
| smb2.cmd == 0x05               | Show only SMB file writes             |
| smb2.cmd == 0x06               | Show only file close operations       |
| `smb2.cmd` == 0x07             | Show only directory queries           |
| smb2.cmd == 0x08               | Show file attribute changes           |
| `smb2.nt_status == 0xc000006d` | Show failed authentication attempts   |

#### **Understanding SMB File Operations in Wireshark**

1️. **Find an SMB `Tree Connect Request`** → Determines which share is accessed (e.g., `\\SERVER\SHARE`).\
2️. **Look for `NT Create AndX Request`** → Shows which files are being accessed.\
3️. **Check `Read Request` and `Write Request`** → Tracks file transfers.\
4️. **Watch for `Close Request`** → Indicates file operation completion.

**Example Wireshark Analysis Flow:**

* Open a PCAP in Wireshark
* Use the filter: `smb2.cmd == 0x03` (to find file reads)
* Right-click a packet → `Follow → TCP Stream` to view the conversation

#### **SMB Authentication and Sessions**

| **Stage**           | **Packet Type**                   | **Wireshark Filter**      |
| ------------------- | --------------------------------- | ------------------------- |
| **Handshake**       | `Negotiate Protocol Request`      | `smb2.cmd == 0x00`        |
| **Authentication**  | `Session Setup Request`           | `smb2.cmd == 0x01`        |
| **Access Shares**   | `Tree Connect Request`            | `smb2.cmd == 0x03`        |
| **File Operations** | `NT Create AndX`, `Read`, `Write` | `smb2.cmd in {0x05,0x06}` |

**SMB Authentication Types:**

* **NTLMv1 / NTLMv2** → Older authentication methods
* **Kerberos** → Used in Active Directory environments

### **8. Common SMB Use Cases**

| **Scenario**                       | **Wireshark Filter**                                   |
| ---------------------------------- | ------------------------------------------------------ |
| **Find SMB traffic**               | `tcp.port == 445`                                      |
| **Identify file reads**            | `smb2.cmd == 0x03`                                     |
| **Find failed logins**             | `smb2.nt_status == 0xc000006d`                         |
| **Check access to shared folders** | `smb2.cmd == 0x03 && smb2.share_name contains "SHARE"` |
| **Monitor SMB file transfers**     | `smb2.cmd in {0x03,0x05}`                              |

### **10. SMTP (Simple Mail Transfer Protocol)**&#x20;

**Purpose:** SMTP is used to **send emails** between mail servers and email clients. It defines how messages are sent, relayed, and delivered over the internet.

**Common Ports:**

* **25** → Default SMTP (sometimes blocked to prevent spam)
* **587** → SMTP with STARTTLS (secure submission)
* **465** → SMTP over SSL (legacy secure SMTP)\
  Protocol Type: Text-based, request-response over TCP\
  Primary Function: Sending (not receiving) emails.

#### **How SMTP Works**

1️. **Client initiates connection** → `HELO` or `EHLO`\
2️. **Server responds with greeting** → "250 OK"\
3️. **Client starts mail transaction** → `MAIL FROM: sender@example.com`\
4️. **Recipient is specified** → `RCPT TO: recipient@example.com`\
5️. **Message body is sent** → `DATA` → (Message content) → `.`\
6️. **Server confirms delivery** → `250 OK`\
7️. **Client terminates session** → `QUIT`

{% hint style="info" %}
If encryption is supported, STARTTLS is used to switch to a secure connection.
{% endhint %}

#### **Key SMTP Packet Fields in Wireshark**

| **Field**   | **Description**                                |
| ----------- | ---------------------------------------------- |
| HELO / EHLO | Client greeting (EHLO supports more features). |
| MAIL FROM   | Sender's email address.                        |
| RCPT TO     | Recipient's email address.                     |
| DATA        | Begins the email message body.                 |
| . (dot)     | Marks the **end** of the email body.           |
| 250 OK      | Server confirms command success.               |
| STARTTLS    | Switches to encrypted communication.           |
| QUIT        | Ends the SMTP session.                         |

#### **Wireshark Filters for SMTP**

| **Filter**                                 | **Description**                              |
| ------------------------------------------ | -------------------------------------------- |
| smtp                                       | Show all SMTP traffic.                       |
| tcp.port `== 25`                           | Show only traffic on port 25 (default SMTP). |
| tcp.port == 587                            | Show SMTP submission (STARTTLS encryption).  |
| tcp.port == 465                            | Show SMTP over SSL.                          |
| smtp.req.command == "MAIL"                 | Show email sender addresses.                 |
| smtp.req.command == "RCPT"                 | Show email recipient addresses.              |
| smtp.req.parameter contains "@example.com" | Find emails sent to a specific domain.       |

#### **SMTP Authentication in Wireshark**

| **Authentication Type** | **Description**                               |
| ----------------------- | --------------------------------------------- |
| AUTH LOGIN              | Uses Base64-encoded username/password.        |
| AUTH PLAIN              | Sends credentials in plain text (not secure). |
| AUTH CRAM-MD5           | Uses challenge-response authentication.       |

**Find login attempts with Wireshark:**

* Use filter: `smtp.req.command == "AUTH"`
* Look for Base64-encoded credentials (can be decoded manually).

#### **SMTP Email Contents in Wireshark**

1️. **Find `DATA` packets** (`smtp.req.command == "DATA"`)\
2️. **Follow the TCP stream** (`Right-click → Follow → TCP Stream`)\
3️. **Look for email headers and body**

Typical email headers found in SMTP traffic:

```
From: sender@example.com  
To: recipient@example.com  
Subject: Test Email  
Date: Thu, 29 Feb 2024 12:00:00 +0000  
Message-ID: <ABC123@example.com>  
```

#### **Understanding SMTP Response Codes**

| **Code** | **Meaning**                              |
| -------- | ---------------------------------------- |
| `220`    | Server ready.                            |
| `250`    | Command accepted.                        |
| `354`    | Start email content (after `DATA`).      |
| `421`    | Server closing connection.               |
| `450`    | Temporary failure (mailbox unavailable). |
| `550`    | Permanent failure (user doesn't exist).  |

#### **Common SMTP Use Cases**

| **Scenario**                      | **Wireshark Filter**                         |
| --------------------------------- | -------------------------------------------- |
| **Show all SMTP traffic**         | `smtp`                                       |
| **Find email senders**            | `smtp.req.command == "MAIL"`                 |
| **Find email recipients**         | `smtp.req.command == "RCPT"`                 |
| **Identify unencrypted logins**   | `smtp.req.command == "AUTH"`                 |
| **Detect outgoing email domains** | `smtp.req.parameter contains "@example.com"` |
