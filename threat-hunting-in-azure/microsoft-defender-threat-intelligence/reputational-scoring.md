# Reputational Scoring

## Overview:

The following section provides an overview of Microsoft Defender TI Reputational Scoring.&#x20;

### Microsoft Defender Threat Intelligence (Defender TI) Reputation Scoring

**Microsoft Defender Threat Intelligence (Defender TI)** provides reputation scores for hosts, domains, or IP addresses to quickly assess their trustworthiness and detect any ties to malicious or suspicious infrastructure.

### Key Components

1. **Understanding Reputation Scores:**
   * Reputation scores are determined by algorithms designed to quantify the risk associated with an entity.
   * Scores range from 0 to 100, with higher scores indicating higher risk.
2. **Scoring Brackets:**
   * **75+ Malicious:** Confirmed associations with known malicious infrastructure.
   * **50-74 Suspicious:** Likely association with suspicious infrastructure based on machine learning rules.
   * **25-49 Neutral:** Matches at least two machine learning rules.
   * **0-24 Unknown (Green):** Returned at least one matched rule.
   * **0-24 Unknown (Grey):** No rule matches.
3. **Detection Methods:**
   * Factors include known associations with blocklisted entities and machine learning rules.
   * Examples of rules include self-signed TLS certificates, suspicious name servers, and specific registrars or email providers.
4. **Severity Ratings:**
   * Rules are assigned severity levels (High, Medium, Low) based on the risk they represent.
5. **Use Cases:**
   * **Incident Triage, Response, and Threat Hunting:**
     * Use reputation scores to assess if an IP address or domain is good, suspicious, or malicious.
     * For unknown or neutral indicators, deeper investigation is encouraged using Defender TI data sets.
     * Review articles associated with reputation scores for more context on potential threats.
   * **Intelligence Gathering:**
     * Share associated articles with threat intelligence teams to understand potential threats targeting their organization.

Detection Rules and Examples:

* **TLS Certificate Self-Signed:** Indicates potential malicious behavior.
* **Tagged as Malicious:** By an organization member.
* **Web Components Observed:** Number of components might indicate maliciousness.
* **Name Server:** Usage by domains likely to be malicious.
* **Registrar:** Likelihood of domains being malicious based on the registrar.
* **Registrant Email Provider:** Likelihood of registering malicious domains.

Important Note:

As of June 30, 2024, the standalone Defender TI portal will be retired. Customers should use Defender TI within the Microsoft Defender portal or with Microsoft Copilot for Security.
