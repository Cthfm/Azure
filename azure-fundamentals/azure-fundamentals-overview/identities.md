# Identities

## Overview

Azure supports various identity types, each designed to manage access and permissions for different resources and scenarios.&#x20;

Here's an overview of the primary identity types in Azure:

### 1. **User Identity**

* **Description**: This identity represents an individual user with an account in Azure Active Directory (Azure AD). These users can be employees, contractors, or external collaborators.
* **Use Case**: User identities are used when a person needs to interact with Azure resources, such as logging into the Azure portal, accessing Office 365 apps, or managing cloud resources.
* **Example**: A developer logging into the Azure portal to manage a virtual machine.

### 2. **Service Principal**

* **Description**: A **Service Principal** is a non-human identity associated with an application or service that needs to access Azure resources. It is created automatically when you register an application in Azure AD.
* **Use Case**: This is commonly used by applications, automation scripts, or services that need to authenticate and access resources programmatically. It ensures that applications can interact with resources without requiring user login.
* **Example**: A CI/CD pipeline using a service principal to deploy infrastructure in Azure automatically.

### 3. **Managed Identity**

* **Description**: Managed Identities are special types of identities assigned to Azure resources like VMs, App Services, or Azure Kubernetes Service (AKS) clusters. They allow these resources to authenticate and access other Azure resources securely, without storing credentials.
* **Types**:
  * **System-assigned**: Automatically created and deleted when the resource is created or deleted.
  * **User-assigned**: A reusable managed identity that can be assigned to multiple resources.
* **Use Case**: Ideal for securing communications between Azure resources by avoiding hardcoded credentials or secrets.
* **Example**: A virtual machine that needs to access a storage account via its managed identity.

### 4. **Workload Identity**

* **Description**: Workload Identity is a newer feature specifically designed for Kubernetes environments. It allows Kubernetes workloads to authenticate to Azure resources using Azure AD without needing secrets or certificates. It integrates Kubernetes Service Accounts (KSA) with Azure Active Directory.
* **Use Case**: When workloads running in Azure Kubernetes Service (AKS) need secure access to other Azure services like Azure Key Vault or Blob Storage without storing secrets.
* **Example**: A Kubernetes pod using its service account to authenticate to Azure Blob Storage.

### 5. **Application Identity**

* **Description**: When you register an application in Azure AD, it is assigned an **Application Identity**, which is essentially the **Service Principal** tied to the application. This allows the app to authenticate and interact with Azure resources securely.
* **Use Case**: This is used when an application needs to authenticate and access resources without user interaction. Applications can either act on their own behalf or on behalf of users.
* **Example**: A web application that authenticates with Azure AD to retrieve user data from the Microsoft Graph API.

### 6. **Device Identity**

* **Description**: This identity represents a physical device, such as a laptop or mobile device, registered with Azure AD. These devices can be controlled and managed as part of an organization's security policies.
* **Use Case**: Device identities are used to enforce Conditional Access policies, ensuring that only compliant and secure devices can access organizational resources.
* **Example**: A corporate laptop that complies with security policies and is used to access corporate email or internal applications.

### 7. **Guest Identity**

* **Description**: Guest identities are external users who are invited to collaborate within an organization's Azure AD tenant. These users have limited access to resources compared to internal users.
* **Use Case**: Used for B2B (business-to-business) collaboration where external partners, vendors, or contractors need access to specific resources.
* **Example**: A contractor being granted access to an internal SharePoint site.

### 8. **Group Identity**

* **Description**: Groups in Azure AD are collections of users that simplify the management of permissions. Instead of assigning permissions individually, you can assign them to a group.
* **Use Case**: Ideal for role-based access control (RBAC), where permissions are assigned to a group of users that share similar responsibilities.
* **Example**: A security group called "Developers" that has access to a resource group within Azure.

### Key Use Cases for Each Identity Type:

* **User Identity**: For individuals who need to interact with Azure resources manually (e.g., logging into the Azure portal).
* **Service Principal**: For non-human users like applications or services that need to access resources programmatically.
* **Managed Identity**: For securing communications between Azure resources without handling credentials (e.g., a VM accessing Azure Key Vault).
* **Workload Identity**: For Kubernetes workloads needing secure access to Azure resources without storing secrets (e.g., a Kubernetes pod accessing Blob Storage).
* **Application Identity**: For applications that need to authenticate to Azure AD and access resources on their own or on behalf of users.
* **Device Identity**: For managing devices and ensuring only compliant devices can access corporate resources.
* **Guest Identity**: For external users who need limited access to collaborate on specific resources.
* **Group Identity**: For simplifying role management by assigning permissions to a group of users.
