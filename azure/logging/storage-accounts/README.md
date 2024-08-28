# Storage Accounts

## Storage Account Overview

A storage account in Azure is a container that provides a unique namespace for storing your data in Azure. It gives you access to various Azure Storage services such as Blob storage, File storage, Queue storage, and Table storage. The storage account makes it easy to manage your storage resources, offering a consistent way to manage access, security, and monitoring.

### Features of a Storage Account

1. **Blob Storage**: Designed for storing large amounts of unstructured data such as text or binary data. Blob storage is ideal for serving images or documents directly to a browser, storing files for distributed access, streaming video and audio, writing to log files, and storing backup and restore data.
2. **File Storage**: Provides fully managed file shares in the cloud that are accessible via the Server Message Block (SMB) protocol. This feature allows you to share files across multiple machines and applications and is suitable for legacy applications that require file shares.
3. **Queue Storage**: Offers a messaging solution for storing large numbers of messages. Queue storage is used to decouple and scale applications, allowing asynchronous processing and reliable message delivery between components.
4. **Table Storage**: A NoSQL key-value store for storing large amounts of structured data. Table storage is useful for applications that need a schema-less storage option, providing fast access to data and scalability.
5. **Durability and Availability**: Azure Storage accounts provide high durability and availability with options for locally-redundant storage (LRS), zone-redundant storage (ZRS), geo-redundant storage (GRS), and read-access geo-redundant storage (RA-GRS).
6. **Security**: Offers various security features, including encryption at rest, shared access signatures (SAS), and Azure Active Directory (AAD) integration for fine-grained access control.
7. **Scalability**: Azure Storage accounts are designed to handle large volumes of data and high throughput, allowing you to scale as your needs grow without worrying about capacity limits.
8. **Monitoring and Diagnostics**: Provides comprehensive monitoring and diagnostic features to track the performance and usage of your storage resources. This includes metrics, logs, and integration with Azure Monitor for deeper insights and alerting.
9. **Data Management**: Supports lifecycle management policies to automate the transition of data to the appropriate access tiers based on usage patterns, helping optimize costs.
10. **Integration**: Easily integrates with other Azure services, such as Azure Functions, Azure App Service, and Azure Kubernetes Service (AKS), enabling you to build and deploy complex applications with seamless data storage capabilities.



### Microsoft Documentation

{% embed url="https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview" %}

#### Storage Account Common Error Codes:

{% embed url="https://learn.microsoft.com/en-us/rest/api/storageservices/common-rest-api-error-codes" %}
