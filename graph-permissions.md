# Graph Permissions

## 🛡️ **Why Are Permissions Important?**

Permissions **control what your app can do** and **what data it can access**.

**Without the right permissions:**

* You’ll get `403 Forbidden` errors.
* You may accidentally **expose sensitive data**.
* Your app won’t pass **security reviews** or **compliance audits**.

🔔 In Microsoft Graph, **permissions are everything.**

***

## 📋 **Two Types of Permissions**

| Type                        | Description                                                                          | Common Use Case                                   |
| --------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------- |
| **Delegated Permissions**   | App acts **on behalf of a signed-in user**. User's privileges and limitations apply. | Web and mobile apps where users sign in.          |
| **Application Permissions** | App acts **as itself**. Full access if granted. No user needed.                      | Background services, daemons, automation scripts. |

***

## 🧩 **Understanding Permission Scopes**

When you request an access token, you must specify the **scope** of permissions.

Example (Delegated):

```
pgsqlCopyEditUser.Read
Mail.Read
Group.Read.All
```

Example (Application):

```
pgsqlCopyEditUser.Read.All
Group.ReadWrite.All
Directory.ReadWrite.All
```

***

## 🔐 **How Permissions Are Granted**

| Step | Action                                                  |
| ---- | ------------------------------------------------------- |
| 1    | Developer requests permissions when registering an app. |
| 2    | Users or admins **review** the requested permissions.   |
| 3    | **Consent** is given.                                   |
| 4    | App gets an access token with the approved permissions. |

* **User consent** → For low-privilege operations.
* **Admin consent** → For sensitive operations like reading all users, accessing mailboxes, etc.

***

## 🏛️ **Delegated vs Application Permissions: Real-World Examples**

| Action                                        | Permission Type | Permission Example |
| --------------------------------------------- | --------------- | ------------------ |
| Read signed-in user's profile                 | Delegated       | `User.Read`        |
| Read all users' profiles (no user signed in)  | Application     | `User.Read.All`    |
| Send an email on behalf of the signed-in user | Delegated       | `Mail.Send`        |
| Read all mailbox settings                     | Application     | `Mail.Read`        |

🔔 **Key Point:**\
**Application permissions** are **powerful** and should be carefully restricted.

***

## 🛠️ **Granting Admin Consent (Step-by-Step)**

Sometimes, only an **admin** can approve permissions.

Here’s how you (or your admin) can grant consent:

1. Go to **Azure Portal** → **Microsoft Entra ID** → **App registrations**.
2. Select your app.
3. Go to **API Permissions** → **Add a permission** → **Microsoft Graph** → Choose the required permissions.
4. Click **Grant admin consent**.

✅ This gives the app full authorization to perform those operations without needing a user to approve each time.

***

## 🚨 **Important Security Practices for Graph Applications**

| Practice                        | Why It Matters                                 | Tip                                                            |
| ------------------------------- | ---------------------------------------------- | -------------------------------------------------------------- |
| **Request the least privilege** | Reduce the blast radius if app is compromised. | Only ask for permissions you truly need.                       |
| **Use Conditional Access**      | Control when and where apps can sign in.       | Restrict app logins by location or device compliance.          |
| **Rotate secrets regularly**    | Secrets can leak over time.                    | Rotate client secrets and certificates every 6–12 months.      |
| **Monitor consented apps**      | Old apps can become a security risk.           | Regularly review what apps have permissions in your tenant.    |
| **Log and audit API usage**     | Detect anomalies early.                        | Use Microsoft Entra ID logs and Graph API activity monitoring. |

***

## 📢 **Common Errors Related to Permissions**

| Error                                               | Cause                                     | Solution                                                                 |
| --------------------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------ |
| `403 Forbidden`                                     | Missing permission or no consent granted. | Check app permissions and consent status.                                |
| `Insufficient privileges to complete the operation` | User does not have the required role.     | Use an account with the right Azure AD role (like Global Administrator). |
| `Authorization_RequestDenied`                       | Admin consent required.                   | Have an admin grant consent for the app.                                 |

***

## 🛠️ **Hands-on Exercise: Secure Your App Properly**

| Goal                                        | Action                                                                 |
| ------------------------------------------- | ---------------------------------------------------------------------- |
| Review current permissions                  | Azure Portal → App registrations → API permissions.                    |
| Add `User.Read.All` and grant admin consent | Add under Microsoft Graph → Application permissions.                   |
| Remove unused permissions                   | Clean up permissions you don't actually use.                           |
| Test API call                               | Try a `GET /users` call to confirm your app’s permissions are working. |
