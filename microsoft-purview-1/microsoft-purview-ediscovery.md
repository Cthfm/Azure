# Microsoft Purview eDiscovery

### **Microsoft Purview eDiscovery Overview**

Microsoft Purview eDiscovery (formerly known as Microsoft 365 eDiscovery) is a legal and compliance solution integrated within the Microsoft 365 compliance suite. It is designed to help organizations manage legal investigations, compliance reviews, and discovery of electronically stored information (ESI) across Microsoft 365 services. The goal is to simplify the legal hold, search, collection, review, and export of data for legal and regulatory purposes.

Microsoft Purview eDiscovery is divided into two main offerings:

* **Core eDiscovery**
* **Advanced eDiscovery**

These tiers cater to different levels of organizational requirements, depending on the complexity and scale of legal or compliance investigations.

#### **1. Core eDiscovery**

Core eDiscovery provides essential tools for performing basic legal and compliance investigations within Microsoft 365 environments. It focuses on smaller-scale investigations and includes the following core functionalities:

**Key Features of Core eDiscovery:**

* **Case management**: Users can create cases to track the lifecycle of an investigation.
* **Content search**: Conduct broad or granular searches across multiple Microsoft 365 data sources, such as Exchange mailboxes, SharePoint sites, OneDrive for Business, Teams, and Yammer.
* **Legal holds**: Preserve data in place by placing legal holds on mailboxes, OneDrive accounts, or Teams to ensure the integrity of the data for the duration of an investigation.
* **Export search results**: Export data that has been identified through searches for further analysis or sharing with legal teams or external counsel.

**Use Cases:**

* Handling legal requests related to small investigations.
* Placing holds on data for a limited number of users.
* Collecting and exporting data for external legal counsel.

#### **2. Advanced eDiscovery**

Advanced eDiscovery builds on Core eDiscovery with additional features aimed at larger and more complex investigations. It offers enhanced capabilities to streamline workflows, reduce data volumes, improve analysis, and manage custodian relationships more effectively.

**Key Features of Advanced eDiscovery:**

* **Custodian management**: Track and manage the individuals (custodians) who are the subject of legal holds or whose data is being searched and collected. The custodian workflow helps streamline management of data collection and review processes for specific individuals.
* **Data preservation in-place**: Unlike older eDiscovery processes that require copying and moving data, Advanced eDiscovery preserves the data in its original location (in-place), which ensures compliance and reduces the risk of data tampering.
* **Hold notifications and tracking**: Automatically send notifications to custodians to inform them about the legal hold. The system can track acknowledgments and reminders, ensuring that holds are effectively communicated.
* **Data collection**: Gather data from multiple Microsoft 365 services, such as Exchange Online, SharePoint, OneDrive for Business, Microsoft Teams, Yammer, and more. This ensures all relevant ESI (electronically stored information) is covered.
* **Early case assessment (ECA)**: This allows investigators to quickly identify key information early in the investigation, saving time and reducing data volume before the formal review stage.
* **Review sets**: Organize collected data into manageable sets for detailed review. Tag, search, and filter content in review sets to identify relevant information. Users can apply custom tags and organize data based on case-specific requirements.
* **Advanced analytics and machine learning**: Advanced eDiscovery incorporates machine learning and predictive coding to analyze data and classify documents based on their relevance, potentially reducing the volume of data that needs to be reviewed manually.
* **Data redaction**: Protect sensitive information during the review process by applying redactions to remove confidential or personally identifiable information (PII) before sharing data with legal teams or third parties.
* **Relevance tagging**: Classify and tag documents based on their relevance to the case. This enables more efficient review processes.
* **Communication threading**: Review conversations (such as email threads) in context, so users can understand the flow of communication rather than viewing each message individually.
* **Export for external review**: Export processed data and relevant metadata in formats commonly used by external legal and eDiscovery vendors, such as PST (for emails) and other supported formats.
* **Audit logs**: Track all activities and access within eDiscovery cases, providing detailed logs of who accessed or modified information, ensuring compliance and legal defensibility.

**Use Cases:**

* Large-scale investigations that involve many custodians and data sources.
* Legal cases where preserving and analyzing large volumes of data is required.
* Complex eDiscovery needs that require advanced tools like machine learning, relevance tagging, and predictive coding.

#### **Supported Microsoft 365 Services**

Microsoft Purview eDiscovery can search, preserve, and collect data from a variety of Microsoft 365 services:

* **Exchange Online**: Emails, attachments, and calendar items.
* **SharePoint Online**: Files, documents, and site contents.
* **OneDrive for Business**: Files stored in personal OneDrive accounts.
* **Microsoft Teams**: Conversations, chat logs, and files shared in channels.
* **Yammer**: Messages and posts in organizational communities.
* **Other services**: Additional data sources can be accessed, depending on integrations and third-party applications.

#### **eDiscovery Workflow**

The process of conducting an eDiscovery investigation within Microsoft Purview typically follows a structured workflow:

1. **Create a case**: Begin by creating an eDiscovery case, where all activities, searches, holds, and review sets will be tracked.
2. **Identify data**: Use the **Content Search** feature to identify relevant content across Microsoft 365 data sources. Searches can be fine-tuned using filters such as keywords, date ranges, custodians, and specific content types.
3. **Apply legal holds**: If necessary, apply **legal holds** to preserve data relevant to the investigation. Legal holds prevent any alteration or deletion of content until the hold is lifted, ensuring that data remains intact for the investigation.
4. **Collect data**: Gather the identified data from Exchange, SharePoint, OneDrive, Teams, and other sources into review sets for deeper analysis.
5. **Review and analyze**: Investigators review the collected data, tagging content, applying redactions where necessary, and using advanced analytics to identify key documents. Relevance tagging and machine learning models can help surface important documents faster.
6. **Refine and process**: As the review progresses, documents are filtered, tagged, and refined based on their relevance to the case.
7. **Export data**: Once the investigation is complete, data is exported in a format suitable for legal review, often including PST for email data or native file formats for documents.
8. **Close the case**: When all necessary data has been reviewed and exported, the case can be closed. Audits and logs are maintained to ensure compliance with legal and regulatory standards.

#### **Benefits of Microsoft Purview eDiscovery**

1. **Integrated with Microsoft 365**: Purview eDiscovery is tightly integrated with Microsoft 365 services, making it easy to search and preserve content from multiple sources without moving data.
2. **In-place preservation**: Instead of duplicating or moving data, eDiscovery keeps it in its original location while preventing modification or deletion.
3. **Cost-effective**: By reducing the need for third-party tools and enabling in-house discovery, organizations can save time and money on legal and compliance processes.
4. **Scalability**: From small investigations to complex legal cases involving hundreds of custodians and terabytes of data, Microsoft Purview eDiscovery scales to meet the needs of large enterprises.
5. **Automation and AI**: Advanced features such as machine learning and predictive coding help automate tasks and reduce the burden of manually reviewing large volumes of data.
6. **Compliance**: Comprehensive audit logs and built-in compliance features help ensure that all legal, regulatory, and industry-specific standards are met.

#### **Limitations**

* **Licensing**: Advanced eDiscovery features are only available to organizations with higher-tier Microsoft 365 compliance and eDiscovery licensing (e.g., E5 license). Organizations with lower-tier licenses can only access Core eDiscovery features.
* **Third-party data**: While Microsoft Purview eDiscovery is excellent for Microsoft 365 data, it may not support non-Microsoft services as comprehensively. Third-party integrations or tools may be necessary for those scenarios.
