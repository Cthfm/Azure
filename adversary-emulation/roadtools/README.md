# RoadTools

## **Overview**

**RoadTools** is an open-source toolkit used for security research and penetration testing of **Microsoft Entra ID (formerly Azure AD)** environments. It is particularly useful for **enumeration, analysis, and attack simulations** on Azure AD. Developed by **Dirk-jan Mollema**, a well-known security researcher, RoadTools provides both an **API client** for interacting with Azure AD and a **roadrecon tool** to visualize and explore the data obtained from Azure AD tenants.

### **Key Components**

1. **RoadLib (API Client Library)**
   * A Python library to interact with Microsoft Entra ID.
   * Facilitates making queries against the **Microsoft Graph API**.
   * Automates **token acquisition** and **authenticating against Azure AD** using service principal credentials or OAuth tokens.
2. **RoadRecon (Enumeration and Analysis Tool)**
   * Pulls data from **Azure AD tenants** and stores it in a **local SQLite database**.
   * Enumerates various objects in Entra ID, such as:
     * Users
     * Groups
     * Roles and role assignments
     * Service principals (SPNs)
     * Applications and permissions
     * Conditional Access policies
   * Includes **graphical exploration** tools to view relationships between objects, like **user memberships and role assignments**.

### ROADTools GitHub

{% embed url="https://github.com/dirkjanm/ROADtools" %}
