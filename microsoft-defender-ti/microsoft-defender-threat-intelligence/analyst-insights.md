# Analyst Insights

#### Overview of Analyst Insights in Microsoft Defender Threat Intelligence (Defender TI)

**Microsoft Defender Threat Intelligence (Defender TI)** provides an **Analyst Insights** section that offers quick, relevant information about an artifact, which can be critical for determining the next steps in an investigation. This section lists applicable insights for the artifact and notes insights that don't apply, providing comprehensive visibility.

#### Key Features of Analyst Insights:

1. **Quick Determination:**
   * Insights help quickly assess key details about an artifact. For example, you can determine if an IP address is routable, whether it hosts a web server, or if it had an open port within the past five days.
2. **Inclusive Information:**
   * The system also displays rules that weren't triggered, which can be useful when starting an investigation, as it helps in understanding what is not associated with the artifact.

#### Types of Analyst Insights and Questions Addressed:

1. **Blocklisted:**
   * Is/When was the domain, host, or IP address blocklisted?
   * How many times has Defender TI blocklisted the domain, host, or IP address?
2. **Registered and Updated:**
   * How many days, months, and years ago was the domain registered?
   * When was the domain WHOIS record updated?
3. **Subdomain IP Count:**
   * How many different IP addresses are associated with the subdomains of the domain?
4. **New Subdomain Observations:**
   * When was the last time Microsoft observed a new subdomain for the domain in question?
5. **Registered and Resolving:**
   * Does the domain queried exist?
   * Does the domain resolve to an IP address?
6. **Number of Domains Sharing the WHOIS Record:**
   * What other domains share the same WHOIS record?
7. **Number of Domains Sharing the Name Server:**
   * What other domains share the same name server record?
8. **Crawled by RiskIQ:**
   * When was this host or domain last crawled by Microsoft?
9. **International Domain:**
   * Is the domain queried for an international domain name (IDN)?
10. **Blocklisted by Third Party:**
    * Is this indicator blocklisted by a third party?
11. **Tor Exit Node Status:**
    * Is the IP address in question associated with The Onion Router (Tor) network?
12. **Open Ports Detected:**
    * When did Microsoft last port scan this IP address?
13. **Proxy Status:**
    * What is the proxy status of this indicator?
14. **Host Last Observed:**
    * Is the IP address in question internet accessible?
15. **Hosts a Web Server:**
    * Does the IP address have a DNS server that uses its resources to resolve the name into it for the appropriate web server?

####
