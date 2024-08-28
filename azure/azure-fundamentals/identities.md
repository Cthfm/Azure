# Identities

## Overview

Azure supports various identity types, each designed to manage access and permissions for different resources and scenarios.&#x20;

Here's an overview of the primary identity types in Azure:

### Identity Resource Types

#### 1. **Azure Active Directory (Azure AD) Users**

Azure AD users represent individual accounts in the Azure Active Directory. They can be employees, guests, or external users with specific roles and permissions.

* **Employee Accounts**: Typically assigned to internal users within an organization.
* **Guest Accounts**: Assigned to users outside the organization to collaborate on resources.
* **External Accounts**: External users from partner organizations.

#### 2. **Service Principals**

A service principal is an identity used by applications, services, or automation tools to access specific Azure resources. It works similarly to a user identity but is intended for applications rather than human users.

* **Application Service Principals**: Used by applications to access resources securely.
* **Managed Service Principals**: Created and managed by Azure services like Azure Kubernetes Service (AKS).

#### 3. **Managed Identities**

Managed identities provide an automatically managed identity in Azure AD for applications to use when connecting to resources that support Azure AD authentication.

* **System-Assigned Managed Identity**: Tied to a specific Azure resource and automatically deleted when the resource is deleted.
* **User-Assigned Managed Identity**: Created as a standalone Azure resource and can be assigned to one or more Azure resources.

#### 4. **Groups**

Groups in Azure AD allow you to manage multiple users' access to resources collectively. Groups can be used for role assignments, policy applications, and more.

* **Security Groups**: Used to manage member and computer access to shared resources for a group of users.
* **Microsoft 365 Groups**: Used for collaboration between users, both inside and outside the organization.

#### 5. **Roles**

Roles in Azure define the permissions for users, groups, or service principals to perform specific actions on Azure resources.

* **Built-in Roles**: Predefined roles such as Owner, Contributor, Reader, etc.
* **Custom Roles**: User-defined roles tailored to specific needs and scenarios.

#### 6. **Azure AD B2B (Business-to-Business)**

Azure AD B2B allows external users to access your organization's applications and resources using their own credentials.

* **Guest Users**: External partners or contractors added to your Azure AD tenant for collaboration.

#### 7. **Azure AD B2C (Business-to-Consumer)**

Azure AD B2C is a separate service for managing identity and access for consumer-facing applications.

* **Consumer Users**: Customers or clients who sign up and sign in to your applications using their own preferred identity providers (e.g., Google, Facebook).

### Key Points

* **Authentication**: Ensures the identity is who they claim to be (e.g., password, multifactor authentication).
* **Authorization**: Determines what the identity can do (e.g., role-based access control).
* **Single Sign-On (SSO)**: Enables users to authenticate once and gain access to multiple applications.
* **Conditional Access**: Provides access control based on specific conditions (e.g., location, device state).
