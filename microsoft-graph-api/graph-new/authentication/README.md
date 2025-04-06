# Authentication

### **How Authentication Works in Microsoft Graph**

Microsoft Graph requires authentication before it will let you access any data.

The authentication happens in two main steps:

1. Prove who you are → using Azure Entra ID
2. Get an Access Token → use this token in API requests.

Without a valid token, your Graph requests will be rejected.

***

### **Types of Authentication**

There are two main types of authentication flows you need to know:

| Type                        | Description                                                                   | Common Use Case                                   |
| --------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------- |
| **Delegated Permissions**   | Your app acts on behalf of a signed-in user.                                  | User-facing apps like web apps or mobile apps.    |
| **Application Permissions** | Your app acts as itself with its own identity. No user needs to be signed in. | Background services, daemons, automation scripts. |

**Delegated Example**:

* A web app that reads the signed-in user's emails.

**Application Example**:

* A security monitoring service that reads all users' security alerts 24/7.

***

### **Azure App Registration**

To use Graph API, you must first register your app in Azure.

This tells Microsoft who your app is and what it can access.

#### Step-by-Step: Registering an App

1. Sign in to Azure Portal [https://portal.azure.com](https://portal.azure.com)
2. Go to Microsoft Entra ID → App registrations → + New registration.
3. Fill out:
   * Name: `GraphAPI-DemoApp`
   * Supported account types: Choose "Accounts in this organizational directory only" (for internal apps).
   * Redirect URI: Leave blank for now (needed later for Delegated flows).
4. Click Register.

***

### Important Values

Once the app is created, **note these values**:

* Application (client) ID → Unique ID of your app.
* Directory (tenant) ID → ID of your Azure tenant.
* Client Secret → Like a password for your app (created separately under "Certificates & Secrets").

***

### **Understanding Access Tokens**

Once your app is registered, it can **request an access token** from **Azure Entra ID**.

Basic flow:

1. App sends its Client ID + Client Secret to Entra ID.
2. Entra ID verifies and returns an Access Token.
3. App sends the token in the Authorization header when calling Graph API.

Example Header:

```http
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJh...
```

The Access Token usually lasts for 1 hour depending on how its configured.

***

### **OAuth 2.0 Authorization Flows**

There are different ways to get tokens, depending on your app type.

| Flow                        | When to Use         | Summary                                                           |
| --------------------------- | ------------------- | ----------------------------------------------------------------- |
| **Authorization Code Flow** | User signs in       | Used for apps that need user context (Delegated permissions).     |
| **Client Credentials Flow** | No user interaction | Used for background apps or automation (Application permissions). |

***

### **Authorization Code Flow (Delegated)**

Used when your app needs to act on behalf of a user.

Steps:

1. Redirect user to Microsoft login page.
2. User signs in and grants permission.
3. App gets an authorization code.
4. App exchanges the code for an access token.

***

### **Client Credentials Flow (Application)**

Used when your app acts on its own without a user.

Steps:

1. App sends its Client ID, Client Secret, and Tenant ID to Entra ID.
2. App receives an access token.
3. App uses the token to access Microsoft Graph.
