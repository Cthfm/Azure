# Azure Threat Research Matrix (ATRM)

## Azure Threat Research Matrix (ATRM)

In previous sections, we discussed the MITRE ATT\&CK framework. While MITRE Att\&ck provides a holistic view of TTPS it does not specifically provide the relevant detection information such as API calls, specific log sources, detection queries, and options to deploy alerts within your Azure Tenant.&#x20;

To address this gap, Microsoft, in collaboration with top Azure security researchers, has developed the **Azure Threat Research Matrix (ATRM)**. This knowledge base is specifically designed to document and organize TTPs relevant to Azure and Azure AD (Entra ID), providing a valuable resource for both offensive and defensive security professionals.

## **What is the Azure Threat Research Matrix (ATRM)?**

The ATRM is essentially a structured guide that details the various ways adversaries might attempt to compromise Azure resources or Entra ID. It serves two key purposes:

1. **Visualization of Azure-Specific TTPs**: The ATRM offers a clear and organized framework that allows you to see how different attack techniques are related to broader tactics, giving you a comprehensive view of potential threats within Azure and Azure AD.
2. **Education on Configuration Risks**: The matrix also educates users about the risks associated with misconfigurations in Azure and Azure AD. By understanding these risks, you can take proactive measures to secure your environment according to best practices.

## **Why the ATRM is Important**

While the MITRE ATT\&CK framework is a powerful tool for understanding cyber threats, it doesn’t specifically address the nuances of Azure and Entra ID. The ATRM fills this gap by focusing exclusively on these environments. This focus is crucial because Entra ID, in particular, is deeply integrated with other Microsoft products, such as Microsoft 365, which introduces unique challenges and opportunities for both attackers and defenders.

For example, the ATRM includes techniques like **AZT303 - Managed Device Scripting**, which explains how attackers might exploit Microsoft Intune (integrated with Azure AD) to execute scripts on devices. This level of detail is essential for security teams working in Azure environments because it provides actionable insights that are directly relevant to their specific context.

**How to Use the ATRM**

The ATRM is organized in a way that makes it easy to navigate and find the information you need:

* **Tactics**: The matrix starts with broad categories called tactics, which represent the high-level goals an adversary might have, such as gaining access to sensitive data or maintaining persistence in your environment.
* **Techniques and Sub-Techniques**: Under each tactic, you’ll find specific techniques and sub-techniques that describe how an adversary might achieve those goals. Each technique has a unique identifier and a brief description, making it easy to understand and reference.
* **Detailed Technique Pages**: When you click on a technique, you’ll be taken to a page that provides more detailed information, including:
  * **Affected Resources**: Which Azure resources are impacted by this technique.
  * **Required Actions**: What steps an adversary would need to take to exploit this technique.
  * **Command Examples**: Examples of commands that could be used to carry out the technique, along with suggestions for how to detect and prevent it.
  * **Additional Resources**: Links to further reading or tools that can help you deepen your understanding or apply the information in practice.

This structure ensures that you can quickly find relevant information and use it to improve your security posture in Azure.

**Practical Application of the ATRM**

The ATRM is not just a theoretical framework—it’s designed to be highly practical. By using the matrix, you can:

* **Map Out Potential Threats**: Use the ATRM to identify potential threats specific to your Azure environment and map them against your current defenses.
* **Develop Detection Strategies**: Leverage the command examples and detection suggestions provided in the matrix to build effective monitoring and alerting mechanisms.
* **Educate Your Team**: Share the ATRM with your team to ensure that everyone has a clear understanding of the unique threats facing your Azure environment and how to defend against them.

## Resource Matrix Github.io

{% embed url="https://microsoft.github.io/Azure-Threat-Research-Matrix/" %}

## Resource Matrix Github Reference

{% embed url="https://github.com/microsoft/Azure-Threat-Research-Matrix" %}
