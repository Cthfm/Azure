# Hands On Threat Hunting Examples

## Hands-On Threat Hunting Labs for Azure

Practical, hands-on experience is crucial for mastering threat hunting in Azure environments. The following labs simulate real-world threat scenarios, allowing you to practice detecting, investigating, and responding to security incidents within Azure.

### **Lab 1: Detecting Unauthorized Azure Portal Access**

**Objective:** Identify and respond to unauthorized access attempts to the Azure portal.

**Setup**

* **Azure Subscription:** Ensure you have access to an Azure subscription with Azure Entra ID and Azure Monitor logs enabled.
* **Audit Logs:** Ensure that logging is enabled for Azure Entra ID sign-in and audit logs.
* **Attack Simulation:** Use a different location or a compromised account to simulate unauthorized access attempts to the Azure portal.

**Exercise Steps**

1.  **Access Sign-In Logs:** Use Azure Monitor or Azure Sentinel to access and search through Azure Entra ID sign-in logs.

    ```kusto
    SigninLogs
    | where ResultType != 0
    | where UserPrincipalName == "unauthorized_user@example.com"
    ```
2. **Analyze the Logs:** Look for signs of unauthorized access attempts, such as failed logins, suspicious IP addresses, or logins from unusual locations.
3. **Investigate the Source:** Identify the user or application attempting unauthorized access, and investigate the IP address or location from which the attempts originated.
4. **Response Actions:** Take appropriate response actions, such as blocking the suspicious IP address using Network Security Groups (NSGs) or Conditional Access policies, and investigate the compromised account.

**Discussion**

* What patterns did you identify that indicated unauthorized access?
* How can you automate the detection of such events in a real-world environment?

### **Lab 2: Azure Virtual Machine (VM) Breakout Detection**

**Objective:** Detect and respond to a breakout attempt from an Azure VM.

**Setup**

* **Azure VM:** Deploy a VM in your Azure environment with logging enabled.
* **Security Tools:** Install Microsoft Defender for Cloud and Sysmon for enhanced monitoring.
* **Attack Simulation:** Use a known vulnerability or a custom script to simulate a breakout attempt from the VM.

**Exercise Steps**

1.  **Monitor with Defender for Cloud:** Ensure Defender for Cloud is configured to monitor VM activity and alert on suspicious actions, such as attempts to access the host system.

    ```powershell
    Set-AzVMExtension -ResourceGroupName "ResourceGroup" -VMName "VMName" -Name "MicrosoftAntimalware" -Publisher "Microsoft.Azure.Security" -Type "SecurityMonitoring"
    ```
2. **Simulate the Breakout:** Execute the breakout script within the VM. Observe how Defender for Cloud detects the breakout attempt.
3. **Respond to the Alert:** Upon receiving the alert, investigate the VM and isolate it from the network to prevent further damage.
4. **Forensic Analysis:** Perform a forensic analysis on the VM using Sysmon logs and Azure Security Center. Look for unauthorized file access or changes to critical system files.

**Discussion**

* How did Defender for Cloud help in detecting the breakout attempt?
* What additional measures could you implement to prevent VM breakouts?

### **Lab 3: Detecting Data Exfiltration in Azure Storage**

**Objective:** Identify and respond to a data exfiltration attempt from Azure Storage.

**Setup**

* **Azure Storage Account:** Create a storage account and enable diagnostic logging.
* **Sensitive Data Simulation:** Upload sensitive data to an Azure Blob container and ensure logging is configured to track data access and network activity.
* **Attack Simulation:** Simulate an attack where data is exfiltrated using a script that downloads data from the storage account and sends it to an external IP address.

**Exercise Steps**

1.  **Monitor Access Logs:** Use Azure Monitor or Azure Sentinel to monitor access logs for the storage account.

    ```kusto
    StorageBlobLogs
    | where OperationName == "GetBlob"
    | where ClientIP == "SuspiciousIP"
    ```
2. **Identify Anomalous Transfers:** Look for large or unexpected data transfers, particularly to external IP addresses. Use the logs to trace the source and destination of the data.
3. **Investigate Data Access:** Review access logs to determine how the data was accessed. Identify the user or process responsible for initiating the data transfer.
4. **Response Actions:** Stop the data transfer by revoking access, blocking the destination IP address using NSGs, and rotating access keys if they were compromised.

**Discussion**

* What indicators suggested that data exfiltration was taking place?
* How can you improve detection and prevention of data exfiltration in your Azure environment?

### **Lab 4: Persistent Threat Detection on Azure VMs**

**Objective:** Detect and mitigate a persistent threat within an Azure VM.

**Setup**

* **Azure VM:** Ensure your VM is set up with the necessary security configurations, including Defender for Cloud and custom logging agents like Sysmon.
* **Malware Simulation:** Deploy a VM with an image that simulates persistent malware behavior, such as creating outbound connections to a command-and-control server.

**Exercise Steps**

1.  **Monitor VM Activity:** Use Defender for Cloud to monitor the VM for unusual behavior, such as unexpected network connections or high CPU usage.

    ```kusto
    VMConnectionLogs
    | where RemoteIP == "C2ServerIP"
    ```
2. **Detect Malware Activity:** Use Sysmon and Defender for Cloud to detect signs of malware, such as unexpected network connections, high CPU usage, or the creation of suspicious files.
3. **Quarantine and Mitigation:** Once detected, isolate the VM from the network. Remove the VM and delete the infected VM image from your repository.
4. **Analyze the Infection Vector:** Investigate how the malware was introduced. Was it through a compromised VM image, a vulnerability in the application, or another vector?

**Discussion**

* What challenges did you face in detecting the malware?
* How can you ensure that similar malware does not infect your Azure environment in the future?

**Lab 5: Mitigating Denial of Service (DoS) Attacks in Azure**

**Objective:** Detect and mitigate a DoS attack targeting an Azure application.

**Setup**

* **Azure Application:** Deploy an Azure App Service or VM-based application that you can monitor in real-time.
* **Load Testing Tool:** Use a tool like Azure Load Testing or Apache JMeter to simulate a DoS attack by overwhelming the application with requests.
* **Monitoring Setup:** Configure Azure Monitor and Application Insights to monitor key metrics like CPU usage, memory consumption, and request latency.

**Exercise Steps**

1.  **Simulate the DoS Attack:** Use the load testing tool to generate a high volume of requests to the target application, simulating a DoS attack.

    ```bash
    az network ddos-protection create --resource-group "ResourceGroup" --name "MyDdosProtection"
    ```
2. **Monitor Resource Usage:** Use Azure Monitor to observe the application's resource usage during the attack. Identify signs of resource exhaustion, such as increased CPU and memory usage or slowed response times.
3. **Implement Mitigation Strategies:** Respond to the attack by scaling up the application, implementing Azure WAF (Web Application Firewall), or applying rate limiting to mitigate the impact.
4. **Analyze the Attack:** Review logs and metrics to understand the attack's impact. Determine whether it was targeted or random and assess the effectiveness of your mitigation strategies.

**Discussion**

* How did the attack affect the application's performance?
* What steps can you take to prevent or mitigate DoS attacks in the future?

### Conclusion

These hands-on labs provide a practical, in-depth experience in detecting and responding to various security incidents in an Azure environment. By simulating real-world scenarios, you can refine your threat hunting skills, improve your response strategies, and better secure your Azure deployments. The next sections will explore advanced threat detection techniques, incident response automation, and continuous security improvement in Azure environments.
