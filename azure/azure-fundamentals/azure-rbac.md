# Azure RBAC

## **Overview:**

**Azure Role-Based Access Control (Azure RBAC)** is an authorization system built on Azure Resource Manager that provides fine-grained access management for Azure resources. It helps organizations control who has access to Azure resources, what they can do with those resources, and what areas they can access.

## Key Concepts of Azure RBAC

1. **Security Principal (Who)**
   * **Users**: Individual user accounts.
   * **Groups**: Collections of users.
   * **Service Principals**: Applications and services that require access to Azure resources.
   * **Managed Identities**: Automatically managed identities in Azure AD.
2. **Role Definition (What)**
   * A role is a collection of permissions that define what actions can be performed on resources. Roles can be built-in or custom.
   * **Common Built-in Roles**:
     * **Owner**: Full access to all resources, including the right to delegate access.
     * **Contributor**: Create and manage all types of Azure resources but cannot grant access to others.
     * **Reader**: View existing Azure resources.
     * **User Access Administrator**: Manage user access to Azure resources.
3. **Scope (Where)**
   * Scope determines where the access applies. It can be at multiple levels:
     * **Management Group**: A container for organizing subscriptions.
     * **Subscription**: A grouping of resources.
     * **Resource Group**: A container holding related resources.
     * **Resource**: An individual Azure service like a VM or database.

### How Azure RBAC Works

**Role Assignment**:

* A role assignment consists of three elements: security principal, role definition, and scope. This defines "who" has "what" permissions to "where."

1. **Assigning Roles**:
   * To assign a role, combine a security principal, a role definition, and a scope.
   * Example: Assign the Contributor role to a user for a specific resource group.
2. **Inherited Permissions**:
   * Permissions granted at a higher scope (e.g., subscription) are inherited by child scopes (e.g., resource groups and resources within the subscription).
3. **Creating Custom Roles**:
   * If built-in roles do not meet specific needs, custom roles can be created with tailored permissions.
4. **Role Assignment Example**:
   * Suppose you need to grant a database administrator group access to manage SQL databases. You would:
     * Define the group (security principal).
     * Assign the SQL DB Contributor role (role definition).
     * Apply this to the appropriate subscription or resource group (scope).

### Use Cases for Azure RBAC

1. **Resource Management**:
   * Allow a user to manage virtual machines within a subscription.
   * Allow another user to manage network resources.
2. **Access Control**:
   * Enable a user to manage all resources in a specific resource group.
   * Permit an application to access resources within a resource group.
3. **Security and Compliance**:
   * Ensure that when an employee leaves, their access to all Azure resources is automatically revoked through integration with Microsoft Entra ID (Azure AD).
   * Use access reviews and audits to maintain compliance with security policies.

