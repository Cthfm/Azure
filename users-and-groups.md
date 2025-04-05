# Users and Groups

## **Understanding Users and Groups in Microsoft 365**

* **Users** represent people (like employees) in your Microsoft 365 tenant.
* **Groups** are collections of users.
  * Examples: Microsoft 365 groups, security groups, distribution lists.
* Many business processes involve **managing users and groups** dynamically.

**Graph API** allows you to automate these tasks at scale!

***

## 🛠️ **Common Endpoints**

| Resource            | Endpoint                          |
| ------------------- | --------------------------------- |
| Get my profile      | `/me`                             |
| Get all users       | `/users`                          |
| Get specific user   | `/users/{user-id}`                |
| Create user         | `/users`                          |
| Update user         | `/users/{user-id}`                |
| Delete user         | `/users/{user-id}`                |
| Get all groups      | `/groups`                         |
| Get specific group  | `/groups/{group-id}`              |
| Create group        | `/groups`                         |
| Add member to group | `/groups/{group-id}/members/$ref` |

***

## 👤 **Working with Users**

***

#### 🧠 1. **Get All Users**

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/users
```

✅ This will return a list of users in your tenant.

***

#### 🧠 2. **Get a Specific User**

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/users/{user-id}
```

* `{user-id}` can be the user's **object ID**, **UPN** (user principal name), or **email address**.

Example:

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/users/john.doe@yourdomain.com
```

***

#### 🧠 3. **Create a New User**

```http
httpCopyEditPOST https://graph.microsoft.com/v1.0/users
Content-Type: application/json

{
  "accountEnabled": true,
  "displayName": "John Test",
  "mailNickname": "johntest",
  "userPrincipalName": "johntest@yourdomain.com",
  "passwordProfile": {
    "forceChangePasswordNextSignIn": true,
    "password": "Test1234!"
  }
}
```

✅ This will create a brand-new user account!

**Important**: You must have **User.ReadWrite.All** or **Directory.ReadWrite.All** application permissions.

***

#### 🧠 4. **Update a User**

Use `PATCH` to modify only specific fields.

Example: Change a user’s department.

```http
httpCopyEditPATCH https://graph.microsoft.com/v1.0/users/{user-id}
Content-Type: application/json

{
  "department": "Marketing"
}
```

✅ Only the department field will be updated!

***

#### 🧠 5. **Delete a User**

```http
httpCopyEditDELETE https://graph.microsoft.com/v1.0/users/{user-id}
```

✅ Permanently deletes the user account (moves to "soft delete" first in Azure).

***

## 👥 **Working with Groups**

***

#### 🧠 1. **Get All Groups**

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/groups
```

✅ Lists all groups (Microsoft 365 groups, security groups, etc.).

***

#### 🧠 2. **Get a Specific Group**

```http
httpCopyEditGET https://graph.microsoft.com/v1.0/groups/{group-id}
```

✅ Retrieves details of a specific group.

***

#### 🧠 3. **Create a New Group**

Example: Create a **security group**.

```http
httpCopyEditPOST https://graph.microsoft.com/v1.0/groups
Content-Type: application/json

{
  "displayName": "New Security Group",
  "mailEnabled": false,
  "mailNickname": "newsecuritygroup",
  "securityEnabled": true
}
```

✅ Creates a **security-enabled** group (not a Microsoft 365 group).

**Important**:

* For Microsoft 365 groups, set `"groupTypes": ["Unified"]`
* For security groups, set `"securityEnabled": true`

***

#### 🧠 4. **Add Member to a Group**

```http
httpCopyEditPOST https://graph.microsoft.com/v1.0/groups/{group-id}/members/$ref
Content-Type: application/json

{
  "@odata.id": "https://graph.microsoft.com/v1.0/directoryObjects/{user-id}"
}
```

✅ Adds a user to a group.

**Tip**: Adding users to groups is essential for **access control** in Azure and Microsoft 365.

***

#### 🧠 5. **Remove Member from a Group**

```http
httpCopyEditDELETE https://graph.microsoft.com/v1.0/groups/{group-id}/members/{member-id}/$ref
```

✅ Removes a user from a group.

***

## 🚨 **Important Permissions Needed**

| Action                            | Permissions Needed                                                     |
| --------------------------------- | ---------------------------------------------------------------------- |
| Read users/groups                 | `User.Read.All`, `Group.Read.All`                                      |
| Create/update/delete users/groups | `User.ReadWrite.All`, `Group.ReadWrite.All`, `Directory.ReadWrite.All` |
| Add/remove group members          | `GroupMember.ReadWrite.All`                                            |

Always **grant admin consent** for these permissions when using application credentials!
