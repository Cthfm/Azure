# Ransomware (MS Guidance)

### 1. Ransomware Incident Response Playbook

The ransomware incident response (IR) playbook is a guide to help organizations prepare for, detect, and recover from ransomware attacks. It defines roles, response processes, and prevention strategies, following NIST guidelines. Key components include preparation, detection, containment, recovery, and post-incident response. The playbook should be updated regularly, especially after incidents. Microsoft tools like 365 Defender and Sentinel are recommended for detection and response.

{% file src="../.gitbook/assets/Ransomware Incident Response Playbook.pdf" %}

### 2. Detecting human-operated ransomware attacks with Microsoft Defender XDR <a href="#detecting-human-operated-ransomware-attacks-with-microsoft-defender-xdr" id="detecting-human-operated-ransomware-attacks-with-microsoft-defender-xdr"></a>

Resource discusses detecting human-operated ransomware attacks using Microsoft Defender XDR. Unlike commodity ransomware, these attacks are coordinated, involving techniques like phishing and credential theft. Early detection is vital, as it helps minimize damage. Microsoft Defender XDR offers tools to identify these attacks across various systems. Security teams should use features like custom detection rules, advanced hunting, and threat analytics to proactively identify threats. Regular training and preparedness are key to efficiently responding to ransomware incidents.

{% embed url="https://learn.microsoft.com/en-us/defender-xdr/playbook-detecting-ransomware-m365-defender" %}

### 3. Responding to Ransomware Attacks

Provides guidance on ransomware response, focusing on containment, investigation, eradication, and recovery. Containment involves assessing the attack’s scope, isolating compromised systems, and preventing further spread. Investigation focuses on identifying the breach and tracking attacker movements. Eradication includes removing malware, resetting compromised accounts, and isolating attacker control points. Recovery involves restoring files from backups and re-enabling affected services. Microsoft Defender XDR is recommended for managing incidents and ensuring systems are cleaned and secure before resuming operations.

{% embed url="https://learn.microsoft.com/en-us/defender-xdr/playbook-responding-ransomware-m365-defender" %}

### 4. Defending Against Ransomware

This resource outlines strategies to defend against ransomware attacks, focusing on securing remote access, email, endpoints, and accounts. Key recommendations include using Zero Trust policies, multifactor authentication (MFA), and security tools like Defender for Office 365 and Defender XDR. It also emphasizes maintaining software updates, enforcing strong password policies, and monitoring for deviations from security baselines. The article advocates for centralized configuration of firewalls, utilizing Threat Intelligence to block known threats, and continuously educating users on cybersecurity best practices to minimize ransomware risks.

{% embed url="https://learn.microsoft.com/en-us/security/ransomware/protect-against-ransomware-phase3" %}

### 5. Backup and restore plan to protect against ransomware <a href="#backup-and-restore-plan-to-protect-against-ransomware" id="backup-and-restore-plan-to-protect-against-ransomware"></a>

The resource outlines strategies for protecting against ransomware, emphasizing robust backup and restore plans. It recommends using Azure Backup to secure data and ensure recovery, identifying critical systems, and migrating to the cloud. During an attack, focus on restoring business-critical systems and ensuring clean backups. Post-attack, conduct root cause analysis and update recovery plans. Key practices include validating backups, using offline storage, and leveraging tools like Microsoft Defender XDR for enhanced protection.

{% embed url="https://learn.microsoft.com/en-us/azure/security/fundamentals/backup-plan-to-protect-against-ransomware" %}

### 6. Azure Firewall Premium

Azure Firewall Premium protects against ransomware by providing advanced intrusion detection and prevention (IDPS), inspecting both application and network traffic. It updates daily with over 65,000 signatures to detect malicious activities, including encrypted traffic via TLS inspection. The firewall blocks ransomware command-and-control (C\&C) traffic to prevent encryption, and the Threat Intelligence feature blocks known malicious IPs and domains. With centralized firewall configuration and integration with Azure Sentinel, it offers both prevention and detection to safeguard against ransomware attacks.

{% embed url="https://learn.microsoft.com/en-us/azure/security/fundamentals/ransomware-protection-with-azure-firewall" %}

### 7. Limiting Impact of Ransomware Attacks

This resource focuses on limiting the impact of ransomware by securing privileged access and improving detection and response. It recommends enforcing session security, mitigating privilege escalation, and monitoring identity systems. For ransomware detection, tools like Microsoft Defender XDR are emphasized for rapid threat identification and response. The article stresses the importance of a multi-layered security strategy to reduce risks and mitigate damage quickly, with a focus on privileged access management and swift remediation of common attack entry points.

{% embed url="https://learn.microsoft.com/en-us/security/ransomware/protect-against-ransomware-phase2" %}

### 8. Ransomware Preparation: Backup and Recovery

This resource discusses strategies for protecting against ransomware through effective backup and restore planning. It emphasizes the importance of identifying critical systems, creating regular backups, and using tools like Azure Backup for secure, offsite storage. Key steps before and during an attack include validating backups, using multi-factor authentication for access, and employing disaster recovery planning. During an attack, the focus is on quickly isolating and removing malware, restoring systems from secure backups, and preventing further spread. Post-attack actions involve learning from the incident to enhance future response efforts.

{% embed url="https://learn.microsoft.com/en-us/security/ransomware/protect-against-ransomware-phase1" %}

