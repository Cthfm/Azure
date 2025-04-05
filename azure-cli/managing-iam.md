# Managing IAM

## 6.1 What is Azure Identity and Access Management (IAM)?

**Azure IAM** helps you **securely control** who can **access** Azure resources and **what actions** they can perform.

It’s based on:

| Concept      | Meaning                                                        |
| ------------ | -------------------------------------------------------------- |
| **Identity** | Who you are (User, Group, Service Principal)                   |
| **Role**     | What permissions you have (Reader, Contributor, Owner)         |
| **Scope**    | Where you have access (Subscription, Resource Group, Resource) |

✅ **IAM = Identity + Role + Scope**

***

## 🛠️ 6.2 Creating a Service Principal (SP)

A **Service Principal** is like a **"bot account"** that Azure uses for automation and scripts.

***

#### 🛠️ Create a Service Principal

```bash
bashCopyEditaz ad sp create-for-rbac --name myServicePrincipal
```

Output example:

```json
jsonCopyEdit{
  "appId": "xxxx-xxxx-xxxx-xxxx",
  "displayName": "myServicePrincipal",
  "password": "your-generated-password",
  "tenant": "xxxx-xxxx-xxxx-xxxx"
}
```

✅ Save this output — you’ll need the `appId`, `password`, and `tenant` to log in programmatically.

***

#### 🛠️ Create a Service Principal with a specific Role and Scope

```bash
bashCopyEditaz ad sp create-for-rbac \
  --name myServicePrincipal \
  --role Contributor \
  --scopes /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>
```

✅ This limits the SP’s permissions to a specific **Resource Group** instead of the entire subscription.

***

## 🛡️ 6.3 Assigning Roles to Users and Service Principals

Roles control **what actions** an identity can perform.

Some common built-in roles:

| Role Name   | Permissions                                        |
| ----------- | -------------------------------------------------- |
| Owner       | Full control (including managing access)           |
| Contributor | Create and manage resources (cannot manage access) |
| Reader      | View resources only                                |

***

#### 🛠️ Assign a Role to a User or SP

```bash
bashCopyEditaz role assignment create \
  --assignee <object-id-or-app-id> \
  --role Contributor \
  --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>
```

| Parameter    | Purpose                                   |
| ------------ | ----------------------------------------- |
| `--assignee` | User, Group, or Service Principal ID      |
| `--role`     | Role name (Contributor, Reader, etc.)     |
| `--scope`    | Subscription, Resource Group, or Resource |

✅ This gives permissions **only** at the specified **scope**.

***

## 📋 6.4 Listing Role Assignments

View existing role assignments:

```bash
bashCopyEditaz role assignment list --output table
```

✅ Lists who has what role at what scope.

***

#### Filter by a specific user or Service Principal:

```bash
bashCopyEditaz role assignment list --assignee <object-id-or-app-id> --output table
```

***

## 🗑️ 6.5 Removing Role Assignments

Remove a role assignment:

```bash
bashCopyEditaz role assignment delete \
  --assignee <object-id-or-app-id> \
  --role Contributor \
  --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>
```

✅ **Tip:** Always double-check before deleting access!

***

## 💡 6.6 Best Practices for IAM with Azure CLI

| Best Practice                        | Why It Matters                                                    |
| ------------------------------------ | ----------------------------------------------------------------- |
| Follow Least Privilege               | Grant only the permissions needed                                 |
| Use Role-Based Access Control (RBAC) | Assign built-in roles instead of custom policies unless necessary |
| Scope roles properly                 | Assign at the **smallest** necessary scope (resource, RG)         |
| Rotate Service Principal credentials | SP passwords should be rotated regularly                          |
| Avoid using Owner unless necessary   | Too much power can lead to accidental damage                      |

***

## 📝 Module 6 Summary

| Topic                     | Key Points                                        |
| ------------------------- | ------------------------------------------------- |
| Azure IAM basics          | Control who can access Azure and what they can do |
| Create Service Principals | `az ad sp create-for-rbac`                        |
| Assign roles              | `az role assignment create`                       |
| View role assignments     | `az role assignment list`                         |
| Best practices            | Least privilege, use scopes, rotate credentials   |
