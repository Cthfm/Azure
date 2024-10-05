# Microsoft 365 Insider Risk Management Policy Templates

## Insider Risk Management Policy Templates in M365

Insider risk management templates are pre-defined policy conditions that define risk indicators and the risk scoring model used by the policy. Each policy must have a template assigned during creation, and M365 supports up to 20 policies per template. Below are some of the key policy templates available:

### **Data Theft by Departing Users**

This template focuses on detecting data exfiltration typically associated with employees leaving the organization. It uses exfiltration indicators such as downloading files from SharePoint Online, printing documents, or copying data to personal cloud services.

* **Triggering Events**: Resignation or termination dates from the HR connector or Microsoft Entra account deletion.
* **Optional Configuration**: Configure the Microsoft 365 HR connector to import resignation and termination dates.
* **Cloud Services Monitored**: Includes Box, Dropbox, Google Drive, Amazon S3, and Azure.

### **Data Leaks**

Designed to detect accidental or malicious data leaks, this template monitors activities like SharePoint Online data downloads, file sharing, and printing.

* **Triggering Events**: DLP policy activities that create High severity alerts or built-in exfiltration triggers.
* **Optional Configuration**: Assign a DLP policy to trigger indicators for high severity alerts.

### **Data Leaks by Priority Users**

This template is focused on priority users who may pose higher risks due to their access to sensitive information.

* **Triggering Events**: High severity DLP policy alerts or customized indicators.
* **Configuration**: Assign priority user groups in the insider risk settings.

### **Data Leaks by Risky Users (Preview)**

Monitors employees under performance stress (e.g., poor reviews, demotions). It uses risk signals like job status changes or potentially threatening messages.

* **Triggering Events**: Performance reviews or risky messages flagged by Communication Compliance integration.
* **Optional Configuration**: Configure the Microsoft 365 HR connector or Communication Compliance.

### **Security Policy Violations (Preview)**

This template focuses on violations like installing malware or disabling security features on devices. It uses security alerts from Microsoft Defender for Endpoint.

* **Triggering Events**: Security violations detected by Microsoft Defender for Endpoint.
* **Prerequisites**: Enable Defender for Endpoint integration with Microsoft Purview.

### **Patient Data Misuse (Preview)**

Focused on healthcare organizations, this template monitors unauthorized access or export of patient healthcare records.

* **Triggering Events**: Alerts from connected EMR systems and user profile data from the HR connector.
* **Optional Configuration**: Use the Microsoft Healthcare or Epic connector for EMR system alerts.

### **Risky Browser Usage (Preview)**

This template monitors inappropriate web browsing activity that may violate company policies or pose security risks.

* **Triggering Events**: Visits to risky websites as categorized by browsing indicators.
* **Prerequisites**: Configure browser signal detection.

### **Security Policy Violations by Departing Users (Preview)**

This template is designed for users leaving the organization, monitoring for security violations such as disabling security features or installing malware.

* **Triggering Events**: Resignation or termination dates from the HR connector or Microsoft Entra account deletion.
* **Prerequisites**: Defender for Endpoint integration.

### **Security Policy Violations by Priority Users (Preview)**

Monitors priority users for security violations, such as installing harmful software or disabling security features.

* **Triggering Events**: Microsoft Defender for Endpoint alerts.
* **Prerequisites**: Defender for Endpoint integration and priority user group configuration.

### **Security Policy Violations by Risky Users (Preview)**

Monitors users who might be at risk of committing security violations due to employment stressors like demotions or poor reviews.

* **Triggering Events**: HR connector risk indicators or communication compliance risk signals.
* **Prerequisites**: Defender for Endpoint integration and HR connector configuration.

### Policy Template Limits

Each policy template has a limit on the number of users it can effectively support and process for risk activities. The following table provides maximum user limits for each policy template:

| **Policy Template**                           | **In-Scope User Maximum** |
| --------------------------------------------- | ------------------------- |
| General Data Leak                             | 15,000                    |
| Data Leak by Risky Users                      | 7,500                     |
| Data Leak by Priority Users                   | 1,000                     |
| Data Theft by Departing Users                 | 20,000                    |
| Security Policy Violations                    | 1,000                     |
| Patient Data Misuse                           | 5,000                     |
| Risky Browser Usage                           | 7,000                     |
| Security Policy Violation by Priority Users   | 1,000                     |
| Security Policy Violations by Departing Users | 15,000                    |
| Security Policy Violations by Risky Users     | 7,500                     |
