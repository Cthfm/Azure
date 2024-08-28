# Microsoft Defender TI: Copilot Integration

## Overview:

This section discusses the integration fo Microsoft Defender TI and Microsoft Copilot. It explains how Copilot can be leveraged to get specific threat intelligence information to defenders.&#x20;

### Integration of Microsoft Copilot for Security with Microsoft Defender Threat Intelligence

**Microsoft Copilot for Security** is an AI-driven platform designed to assist security professionals by integrating with **Microsoft Defender Threat Intelligence (Defender TI)**. This integration allows Copilot to provide contextual and actionable threat intelligence directly within security workflows, significantly enhancing the capabilities of security teams.

### **Key Aspects of the Integration**

**1. Seamless Access to Defender TI Data**

Copilot for Security taps into the vast data repository of Defender TI, allowing users to query detailed information about threats, including **threat actors**, **indicators of compromise (IOCs)**, **vulnerabilities**, and more. This direct access ensures that the intelligence provided by Copilot is comprehensive, up-to-date, and highly relevant.

For example, a security analyst investigating a suspicious domain could use a prompt like:

* **"Show me threat intelligence data for `malicious.com`."**

Copilot would then pull all relevant information from Defender TI, such as associated IP addresses, WHOIS records, and any known connections to threat actors, giving the analyst a thorough understanding of the domain's potential risks.

**2. Contextual Threat Intelligence**

The integration enables Copilot to deliver contextual intelligence that helps users understand the broader implications of threats. When investigating an incident, for instance, Copilot can provide data on related threat actors, their known tactics, techniques, and procedures (TTPs), and the infrastructure they typically use.

Consider this prompt example:

* **"Tell me more about Silk Typhoon."**

Copilot would retrieve a detailed profile from Defender TI, including the TTPs used by this threat actor, industries they typically target, and known IOCs. This information allows the security team to tailor their defenses specifically to the threat posed by Silk Typhoon.

**3. Enrichment of Threat Hunting Flows**

Copilot enhances threat hunting by enriching it with data from Defender TI. For example, if a threat hunter needs information about a particular IP address, Copilot can provide details such as reputation scores, historical resolutions, and any associated malicious activity.

A prompt like:

* **"Get resolutions for IP address `192.0.2.1`."**

will result in Copilot pulling historical DNS data from Defender TI, showing how that IP address has been used over time, which domains it has resolved to, and any associated threat actor infrastructure. This information can be crucial in identifying potential malicious activity and correlating it with ongoing threats.

**4. Promptbooks and Pre-Built Prompts**

To make accessing Defender TI's rich data easier, Copilot for Security includes **promptbooks**—collections of predefined prompts that guide users in retrieving specific intelligence. These promptbooks cover various scenarios, such as generating threat actor profiles or assessing the impact of known vulnerabilities.

For instance, using the promptbook, a user might ask:

* **"Generate a vulnerability impact assessment for CVE-2021-44228."**

Copilot would then generate a report summarizing the intelligence from Defender TI about this particular vulnerability, including affected technologies, known exploits, and mitigation steps. This feature is especially useful for security teams needing quick, actionable insights without manually sifting through data.

**5. Operational Efficiency**

The integration allows security teams to utilize Copilot directly within the Microsoft Defender portal, seamlessly incorporating Defender TI's intelligence into their day-to-day operations. This reduces the time and effort required to gather and analyze threat data, allowing teams to respond more quickly and effectively to emerging threats.

For example, a security operations center (SOC) analyst could use a prompt like:

* **"Summarize the latest threats related to my organization."**

Copilot would then use Defender TI to gather and summarize relevant threat intelligence, highlighting the most pressing threats based on the organization's exposure. This capability enables the SOC to prioritize incidents that require immediate attention, improving overall security posture.

### **Using Copilot for Security with Defender TI: Practical Examples**

Here are a few practical prompts you can use within Copilot to leverage Defender TI's capabilities:

* **Threat Actor Analysis:**
  * **"Share the IOCs associated with Silk Typhoon."**
  * **"What TTPs are linked to the Lazarus Group?"**
* **Vulnerability Insights:**
  * **"Summarize the vulnerability CVE-2021-44228."**
  * **"Show me threat actors associated with CVE-2021-44228."**
* **Infrastructure Intelligence:**
  * **"Get reputation data for the host `example.com`."**
  * **"Show me the latest threat articles related to ransomware."**
