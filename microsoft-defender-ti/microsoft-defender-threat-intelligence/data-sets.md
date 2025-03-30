# Data Sets

## Overview:

The following section provides an overview of the Datasets that are associated with Microsoft Defender TI.&#x20;

### Microsoft Defender TI Datasets&#x20;

Microsoft Defender Threat Intelligence (Defender TI) is a powerful tool designed to help security professionals detect, respond to, and proactively prevent threats by leveraging vast amounts of internet infrastructure data. To effectively use Defender TI, it's essential to understand the different data sets it offers and how they can be used in various security scenarios.

### 1. **Traditional Data Sets**

These data sets provide foundational information that is commonly used in threat intelligence and cybersecurity operations. They include:

* **Resolutions (PDNS):** This data set contains historical DNS resolution records, showing which domains have resolved to specific IP addresses over time. It’s invaluable for tracking the evolution of domain-IP relationships, identifying potential threat infrastructure, and performing time-based correlation.
* **WHOIS Information:** WHOIS records provide registration details for domains, such as the registrar, registrant, and contact information. This data can help link different domains or IP addresses to the same owner, even when privacy protections are in place.
* **TLS/SSL Certificates:** These certificates are used to secure communications between servers and clients. By analyzing TLS certificates, you can identify connections between seemingly unrelated servers based on shared certificates, helping to uncover broader threat actor infrastructure.
* **Subdomains:** Subdomains are extensions of a primary domain and can often reveal additional related infrastructure. Monitoring subdomains can help identify patterns or anomalies that suggest malicious activity.
* **DNS and Reverse DNS:** DNS records, including mail exchange (MX), nameserver (NS), and text (TXT) records, provide insights into how domains are structured and connected. Reverse DNS, which maps IP addresses back to domain names, can further uncover related infrastructure.

### 2. **Advanced Data Sets**

Advanced data sets dive deeper into the nuances of web infrastructure and are particularly useful for uncovering hidden or sophisticated threat actor activities. These include:

* **Trackers:** Trackers are unique codes embedded in web pages, often used for tracking user interactions. Threat actors may inadvertently reuse these trackers across different malicious sites, allowing analysts to connect these sites and identify the threat actors behind them.
* **Components:** Web components describe the technologies and services running on a website or server. Analyzing these components can help you understand what a website is built on, identify potential vulnerabilities, and trace threat actor infrastructure based on the technologies they use.
* **Host Pairs:** Host pairs represent connections between two pieces of infrastructure (a parent and a child) observed during web crawls. These connections might be simple redirects or more complex relationships like script inclusions. Understanding these relationships can help you identify malicious redirects, skimming attacks, or other nefarious activities.
* **Cookies:** Cookies are small data files used by websites to store user information. By analyzing cookies, you can identify commonalities across different websites, uncovering related infrastructure or tracking malicious activity.
* **Services:** This data set includes information about the services running on specific ports of an IP address, including the application type, version, and status. It’s useful for identifying potentially vulnerable or misconfigured services that could be exploited by attackers.

### **How These Data Sets Support Security Operations**

Understanding and utilizing these data sets can significantly enhance your ability to:

* **Detect and Respond to Threats:** By correlating data across these various sets, you can identify potential threats earlier and respond more effectively.
* **Prioritize Incidents:** Not all threats are equal; these data sets help you determine which incidents require immediate attention based on the infrastructure involved.
* **Proactively Identify Malicious Infrastructure:** Advanced data sets, in particular, allow you to uncover threat actor infrastructure that might otherwise go unnoticed, enabling proactive measures such as adding domains to blocklists before they can be used in attacks.

### **Using Defender TI for Threat Hunting**

When hunting for threats, start by querying these data sets based on known indicators of compromise (IOCs) like domain names, IP addresses, or certificates. From there, pivot through related data—such as WHOIS records or TLS certificates—to expand your view of potential threats. This comprehensive approach helps you build a more complete picture of the threat landscape and identify connections that might not be immediately obvious.
