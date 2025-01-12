# Defense Strategies

### 1. Cloud Administration Command (T1651)

Involves adversaries abusing legitimate cloud administrative tools, such as Azure CLI or PowerShell, to execute malicious commands or manipulate cloud resources.

**Defensive Strategies:**

* **Least Privilege:** Enforce least privilege access for users and roles.
* **Conditional Access:** Implement Conditional Access Policies and MFA for secure authentication.
* **Entra Audit Logs:** Monitor and log administrative actions and API usage.
* **Use Key Vaults**: Secure credentials using Azure Key Vault and rotate secrets regularly.
* **Deploy Defender for Cloud:** Detect anomalies and suspicious activities with Microsoft Defender for Cloud.
* **Restrict Access:** Restrict CLI and API access to trusted networks using NSGs and IP filtering.
* **Managed Identities instead of Static Credentials:** Use Managed Identities instead of static credentials for authentication.
* **Conduct Role Assignment Audits:** Audit role assignments, new accounts, and configuration changes.
* **Conduct Red Team Engagements:** Conduct red team simulations to test defenses and train staff.
* **Log Lifecycle Management:** Enable and retain detailed logs in secure storage for investigations.

### &#x32;**. Command and Scripting Interpreter (T1059)**

Adversaries use interpreters like PowerShell, Bash, or Python to execute malicious commands.

**Defensive Strategies:**

* **Restrict Interpreter Use**: Limit access to interpreters for only authorized users and scripts.
* **Script Block Logging**: Enable PowerShell script block logging and command-line logging for detailed monitoring.
* **Execution Restrictions**: Use AppLocker or Windows Defender Application Control (WDAC) to block unauthorized script execution.
* **Monitor Command Usage**: Set up alerts for unusual usage patterns, such as encoded commands or excessive script execution.
* **Network Controls**: Block outbound connections from interpreters to untrusted IPs or domains.
* **Use Least Privilege** - Ensure users only have access to exactly what they need in order to complete their job tasks.&#x20;

### **3. Cloud API (T1526)**

Adversaries use cloud service APIs to execute commands or perform actions in cloud environments.

**Defensive Strategies:**

* **API Logging and Monitoring**: Enable and analyze logs from cloud services (e.g., Azure Monitor, AWS CloudTrail).
* **Least Privilege Access**: Restrict API permissions to only what is necessary for each role or service.
* **API Security Tools**: Use API gateways or tools like Azure Defender for Cloud to monitor API activities.
* **Anomalous Behavior Alerts**: Detect and alert on unusual API calls, such as those creating resources outside normal hours.

### **4. Serverless Execution (T1648)**

Adversaries execute malicious code in serverless computing environments like Azure Functions.&#x20;

**Defensive Strategies:**

* **Code Review**: Implement secure code review practices for all serverless functions.
* **Resource Policies**: Apply strict permissions on serverless resources to prevent unauthorized deployment or execution.
* **Monitor Deployments**: Set up alerts for unusual deployments or updates to serverless functions.
* **Logging**: Enable detailed function execution logging (e.g., Azure Function logs) to monitor behavior. [https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions?tabs=portal](https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions?tabs=portal)
* **Utilize Least Privilege** - Ensure only users that need access to trigger or utilize Lambda functions where possible.&#x20;

### **5. User Execution (T1204)**

Adversaries trick users into executing malicious files or clicking on harmful links.

* **User Awareness Training**: Educate users about phishing and social engineering tactics through regular training and simulated phishing campaigns.
* **Email and Attachment Protection**: Implement email filtering to block phishing emails and malicious attachments; enable safe link scanning to analyze URLs.
* **File Scanning**: Use antivirus or EDR solutions to scan files for malicious content before execution.
* **Macro Restrictions**: Disable or restrict macro execution in Office documents unless digitally signed by trusted entities.
* **Web Content Filtering**: Use DNS filtering or web proxies to block access to known malicious websites and prevent downloads from untrusted domains.
* **Application Control**: Enforce application whitelisting to allow only approved software to run and implement Controlled Folder Access for critical directories.
* **Privilege Management**: Limit local administrative rights to reduce the impact of malicious execution and implement Just-In-Time (JIT) access for elevated permissions.
* **Endpoint Protection**: Deploy endpoint detection and response (EDR) tools to detect and block malicious file execution and suspicious behavior.
* **Email Authentication**: Configure SPF, DKIM, and DMARC to prevent email spoofing and unauthorized senders.
* **Patch Management**: Regularly update operating systems, browsers, and third-party applications to mitigate vulnerabilities exploited by phishing attacks.
* **Logging and Monitoring**: Enable execution logging and use SIEM tools to analyze user activity and detect anomalous patterns.
* **Incident Response Readiness**: Develop and test incident response playbooks for phishing and malicious file execution scenarios to ensure rapid containment and recovery.

**Malicious Image (T1204.002)**

Adversaries disguise malicious content as benign-looking images or containers.

**Defensive Strategies:**

* **User Awareness Training**: Educate users about phishing and social engineering tactics.
* **File Scanning**: Use antivirus or EDR solutions to scan files for malicious content before execution.
* **Restrict Execution**: Block execution of files from untrusted locations using security tools like AppLocker or Intune.
* **Container Image Scanning**: Use tools like Microsoft Defender for Containers or Trivy to scan container images for vulnerabilities or malicious content.
* **Email Filtering**: Configure email gateways to detect and block malicious attachments or links.
