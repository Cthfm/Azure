# Microsoft Graph API Introduction

### **What is Microsoft Graph API?**

Microsoft Graph API is the gateway to data and intelligence in Microsoft 365.

It provides a single unified endpoint (`https://graph.microsoft.com`) that allows you to interact with:

* Azure Active Directory (users, groups, devices)
* Exchange (emails, calendars)
* SharePoint (files, sites)
* Teams (chats, teams, channels)
* Microsoft Defender (security alerts)
* And many other services.

Instead of learning multiple APIs for each Microsoft service, Graph unifies them under one roof.

***

### **Why Use Microsoft Graph API?**

**Single Endpoint**: One API to interact with all Microsoft 365 services.\
**Automation**: Automate user creation, group management, alert monitoring, and much more.\
**Security Operations**: Query security alerts, investigate incidents automatically.\
**Integration**: Integrate Microsoft 365 data into custom apps, websites, or workflows.\
**Power Modern Apps**: Build powerful business apps that tie together email, calendar, files, users, security, and more.

***

### **Key Concepts**

#### 1. **REST API**

Graph uses REST, which means you interact by sending HTTP requests like:

* `GET` → Read data
* `POST` → Create data
* `PATCH` → Update data
* `DELETE` → Remove data

Example:

```http
GET https://graph.microsoft.com/v1.0/me
```

Returns information about the signed-in user.

***

#### 2. **Permissions and Consent**

You must have permissions to access Graph resources.

* **Delegated permissions**: Acting on behalf of a user (requires user to sign in).
* **Application permissions**: App acts as itself (no user needed).

{% hint style="warning" %}
**Admins often need to grant consent for permissions.**
{% endhint %}

***

#### 3. **Access Tokens**

You authenticate to Graph API using Access Tokens issued by Microsoft Identity Platform (Azure Entra ID).

Without a valid token, Graph API will reject your request.

Example Authorization Header:

```http
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJh...
```
