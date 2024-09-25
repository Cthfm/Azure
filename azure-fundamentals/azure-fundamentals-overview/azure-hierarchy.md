# Azure Hierarchy

## Overview

Azure's hierarchy is structured to organize resources, manage permissions, and control costs. Here is an overview of the main components in the Azure hierarchy:

<figure><img src="https://1.bp.blogspot.com/-l-FiJqsZkFs/Xu_efVGm6YI/AAAAAAAABhI/gtiSj_q5z1cfTHvzb_C_5mANN5TpBFuIwCK4BGAsYHg/s320/azure.png" alt="" width="375"><figcaption></figcaption></figure>

### Hierarchy Resources

#### **1. Tenant (Azure Active Directory)**

* **Top-Level Identity and Directory Service**: The tenant is linked to an instance of Azure Active Directory (Azure AD). It provides identity, access management, and directory services for users, groups, and applications.
* **Single Tenant per Organization**: Typically, an organization will have a single tenant that spans across all its Azure services.

#### **2. Management Groups**

* **Organizational Containers**: Management groups allow you to organize subscriptions into containers. You can apply governance policies and access control across multiple subscriptions.

#### **3. Subscriptions**

* **Billing and Access Control**: Each subscription is linked to a billing account. Subscriptions provide a way to manage and isolate resources and access control. Billing and usage reporting are done at the subscription level.

#### **4. Resource Groups**

* **Logical Containers**: Resource groups are logical containers for resources like virtual machines, databases, and storage accounts. All resources in a resource group should share the same lifecycle and management policies.

#### **5. Resources**

* **Individual Services**: Resources are the actual services you deploy, such as virtual machines, web apps, databases, etc. Each resource is created within a resource group and a specific region.



### **Key Concepts**

* **Tenant (Azure AD)**: Provides identity, access management, and directory services for the entire organization.
* **Management Groups**: Useful for applying policies and RBAC (Role-Based Access Control) across multiple subscriptions.
* **Subscriptions**: Act as boundaries for billing, resource management, and quotas. Each subscription has its own set of policies and RBAC settings.
* **Resource Groups**: Logical grouping of related resources for easier management and lifecycle operations (like deployment, updating, and deleting).
* **Resources**: The actual Azure services you use and manage.

### **Additional Concepts**

* **Azure Active Directory (Azure AD)**: Centralized identity and access management service. It is used to control access to resources in Azure.
* **Policies**: Used to enforce organizational standards and to assess compliance at various scopes: management groups, subscriptions, or resource groups.
* **Role-Based Access Control (RBAC)**: Provides fine-grained access management for Azure resources. Roles can be assigned at different levels (management group, subscription, resource group, or resource).

### **Organization Example**

Suppose your organization is Fintech company and has multiple departments, each with its own set of applications and services:

```
Tenant: FinTech Inc
  ├── Management Group: Root Management Group
        ├── Management Group: Finance
        │     ├── Subscription: Finance-Prod
        │     │     ├── Resource Group: Finance-Prod-RG1
        │     │     └── Resource Group: Finance-Prod-RG2
        │     ├── Subscription: Finance-Dev
        │     │     ├── Resource Group: Finance-Dev-RG1
        │     │     └── Resource Group: Finance-Dev-RG2
        │     └── Subscription: Finance-Test
        │           ├── Resource Group: Finance-Test-RG1
        │           └── Resource Group: Finance-Test-RG2
        ├── Management Group: IT
        │     ├── Subscription: IT-Prod
        │     │     ├── Resource Group: IT-Prod-RG1
        │     │     └── Resource Group: IT-Prod-RG2
        │     ├── Subscription: IT-Dev
        │     │     ├── Resource Group: IT-Dev-RG1
        │     │     └── Resource Group: IT-Dev-RG2
        │     └── Subscription: IT-Test
        │           ├── Resource Group: IT-Test-RG1
        │           └── Resource Group: IT-Test-RG2
        ├── Management Group: Product Development
        │     ├── Subscription: ProdDev-Prod
        │     │     ├── Resource Group: ProdDev-Prod-RG1
        │     │     └── Resource Group: ProdDev-Prod-RG2
        │     ├── Subscription: ProdDev-Dev
        │     │     ├── Resource Group: ProdDev-Dev-RG1
        │     │     └── Resource Group: ProdDev-Dev-RG2
        │     └── Subscription: ProdDev-Test
        │           ├── Resource Group: ProdDev-Test-RG1
        │           └── Resource Group: ProdDev-Test-RG2
        ├── Management Group: Central Services
              ├── Subscription: Central-Shared
              │     ├── Resource Group: Central-Shared-RG1
              │     └── Resource Group: Central-Shared-RG2
              └── Subscription: Central-Security
                    ├── Resource Group: Central-Security-RG1
                    └── Resource Group: Central-Security-RG2

```

#### Key Points:

* **Tenant (FinTech Inc)**: Represents the organization.
* **Root Management Group**: The top-level management group.
* **Finance Management Group**: Contains subscriptions and resource groups for the Finance department.
  * **Finance-Prod, Finance-Dev, Finance-Test**: Subscriptions for production, development, and testing environments within the Finance department.
* **IT Management Group**: Contains subscriptions and resource groups for the IT department.
  * **IT-Prod, IT-Dev, IT-Test**: Subscriptions for production, development, and testing environments within the IT department.
* **Product Development Management Group**: Contains subscriptions and resource groups for the product development teams.
  * **ProdDev-Prod, ProdDev-Dev, ProdDev-Test**: Subscriptions for production, development, and testing environments within the product development teams.
* **Central Services Management Group**: Manages shared services and security resources across the organization.
  * **Central-Shared, Central-Security**: Subscriptions for shared services and security resources.

### Resource Organization Documentation

{% embed url="https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/resource-org" %}
