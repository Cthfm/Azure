# Oh365UserFinder

## Overview

Oh365UserFinder is an open-source reconnaissance tool specifically designed for gathering information about users within a Microsoft 365 (formerly Office 365) environment. It’s used primarily by penetration testers, red teamers, and security professionals for enumeration tasks in cloud-based infrastructures. The tool leverages unauthenticated and authenticated queries to gather details on potential user accounts and other public-facing information within a Microsoft 365 tenant.

### **How It Works**

* Oh365UserFinder takes advantage of Microsoft 365’s public interfaces, such as **login.microsoftonline.com**, to identify valid users within a tenant.
* When a request is made to authenticate a user, Microsoft 365 can respond differently depending on whether the user exists or not. Oh365UserFinder automates this process to **enumerate valid usernames** without requiring full authentication.

### **Types of Enumeration Methods:**

1. **Unauthenticated Enumeration**

* The tool sends HTTP requests to Microsoft 365 login endpoints (e.g., OAuth endpoints) to determine whether a user exists based on the error messages returned.

2. **Authenticated Enumeration**

* If credentials are known or guessed (e.g., service accounts), the tool can use them to **enumerate additional user information** through authenticated queries.

### **Common Use Cases**

* **Penetration Testing:** Identifying valid user accounts before launching **password spray attacks**.
* **Red Team Operations:** Gaining a foothold by enumerating users within an organization.
* **Phishing Campaigns:** Identifying targets within a specific tenant for targeted attacks.

### **Key Features**

* **Tenant Enumeration:** Identifies Microsoft 365 tenants by interacting with public login services.
* **User Enumeration:** Checks whether specific usernames or emails exist within the tenant.
* **Credential Validation:** Tests weak or known passwords (for service accounts or default accounts).
* **Batch Testing:** Supports input lists of usernames or email addresses to **test multiple accounts in bulk**.

### GitHub Link

{% embed url="https://github.com/dievus/Oh365UserFinder" %}
