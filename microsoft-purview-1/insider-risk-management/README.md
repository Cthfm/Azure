# Insider Risk Management

## Overview

Insider Risk Management in Microsoft 365 (M365) is a powerful solution that helps organizations identify, investigate, and manage insider threats across Microsoft’s ecosystem. This feature is part of Microsoft Purview and is specifically designed to detect malicious or inadvertent activities by users that could lead to data leaks, compliance violations, or security incidents.

### Key Features of Insider Risk Management in M365:

1. **Risk Indicators and Policies**:
   * **Pre-built risk indicators**: Microsoft Purview has built-in indicators such as data leakage, data theft, or suspicious file transfers that help detect and flag risky user behavior. These indicators can be customized based on your organization's needs.
   * **Customizable policies**: You can set up policies to monitor specific behaviors or actions, such as downloading large amounts of data, accessing confidential files, or using third-party services like email or cloud storage to move sensitive information.
2. **Integration with Other M365 Tools**:
   * **Microsoft Defender for Endpoint**: Provides integration to enhance the detection and investigation of security incidents, especially when it involves devices in your network.
   * **Microsoft Cloud App Security (MCAS)**: Detects and monitors the use of third-party applications that could be used for data exfiltration.
   * **Microsoft Teams**: Insider Risk Management can monitor actions within Teams to detect improper data sharing or communication of sensitive information.
3. **User Privacy Protections**:
   * Insider Risk Management anonymizes user identities during investigations to maintain privacy until the investigation requires deeper scrutiny. Only authorized investigators can de-anonymize users when evidence of suspicious activity is confirmed.
4. **Risk Scoring and Analytics**:
   * Each user’s actions are assigned a risk score based on predefined thresholds. Higher scores may indicate a higher level of threat, allowing security teams to prioritize investigations.
   * Historical trends and analytics help monitor ongoing risk behaviors and highlight patterns of concern.
5. **Workflows and Case Management**:
   * **Case creation**: When suspicious activity is detected, a case is created, which includes all relevant information and allows security teams to review the evidence.
   * **Investigation tools**: Within the Insider Risk Management dashboard, you have the ability to review alerts, analyze file transfers, and review communications to gather a full picture of the incident.
   * **Escalation**: If the investigation reveals a true insider threat, you can escalate the case to HR, legal, or law enforcement as needed.
6. **Data Sources**:
   * **Unified Audit Logs (UAL)**: Insider Risk Management leverages the Unified Audit Logs in M365 to monitor file activities, email, and other services for unusual behavior.
   * **Data from SharePoint, OneDrive, Exchange Online**: Insider Risk Management scans activities within core services like SharePoint and OneDrive to detect sensitive file movements and abnormal file sharing.
7. **Machine Learning and Behavioral Analytics**:
   * Microsoft's solution utilizes machine learning to detect anomalies in user behavior based on established baselines for typical activities. Behavioral analytics can highlight when users act outside of normal patterns, flagging potential threats early.
8. **Actionable Insights**:
   * The platform provides actionable insights to help security and compliance teams respond to risks before they become incidents. This includes suggestions on remediation actions such as revoking access or increasing monitoring of specific individuals.

### Example Use Cases:

1. **Data Exfiltration Prevention**: Insider Risk Management can flag when an employee starts uploading large files from OneDrive or SharePoint to external storage services shortly before leaving the organization.
2. **IP Theft Detection**: It can detect patterns that indicate an employee is attempting to steal intellectual property (e.g., copying proprietary documents from SharePoint or Teams to a personal device).
3. **Compliance Violations**: Insider Risk Management can monitor for actions that may violate regulatory requirements, such as sharing confidential data externally or accessing restricted information without permission.

Incorporating Insider Risk Management in M365 as part of a broader security strategy can help organizations maintain a secure, compliant environment while managing insider risks efficiently.
