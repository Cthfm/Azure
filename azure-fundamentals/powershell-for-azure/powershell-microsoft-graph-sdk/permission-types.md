# Permission Types

## Overview:&#x20;

The Microsoft Graph SDK uses two main permission types: **Delegated Permissions** and **Application Permissions**. **Delegated Permissions** are used by apps acting on behalf of a signed-in user, requiring user consent and limited by the user's own permissions. **Application Permissions** are for apps running without user interaction, like background services, requiring admin consent and offering broader access across an organization. Both permission types ensure secure and controlled access to Microsoft 365 resources.

## Delegated Permissions

* **User Context**: Requires a signed-in user.
* **Scope**: Limited to what the signed-in user can access.
* **Consent**: Typically requires user consent.
* **Use Case**: User-facing apps performing actions on behalf of the user.
* **Examples**:
  * Reading and sending the user’s emails.
  * Accessing the user’s calendar and files.

## Application Permissions

* **User Context**: No signed-in user required.
* **Scope**: Can access data across the entire organization.
* **Consent**: Requires explicit admin consent.
* **Use Case**: Background services or daemons needing broad access.
* **Examples**:
  * Accessing all users' emails for compliance.
  * Automating user account management.
