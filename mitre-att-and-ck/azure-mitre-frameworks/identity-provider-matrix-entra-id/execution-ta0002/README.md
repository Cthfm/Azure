# Execution: TA0002

## **Execution Techniques in Entra ID (Azure Identity Environments)**

In Entra ID (Microsoft Azure Active Directory), adversaries use Execution techniques to **run code, manipulate resources, or trigger actions** post-initial access.\
Unlike traditional endpoints, **execution in Entra ID is almost always API-driven** — by abusing **Azure Management APIs** to control users, groups, roles, or resources.

***

#### 💻 Command and Scripting Interpreter → Cloud API

\| MITRE ID | **T1059.009** (Command and Scripting Interpreter → Cloud API) |

**Description**:\
Use Azure AD and Microsoft Graph APIs (or Azure Resource Manager APIs) to execute administrative operations, manipulate identities, modify configurations, or trigger downstream effects across cloud resources.

**Entra ID Example**:

* An attacker uses stolen OAuth tokens or compromised credentials to run Microsoft Graph API calls to create users, assign roles, or modify directory objects.

```bash
bashCopyEdit# Create a new Entra ID user via Graph API
curl -X POST https://graph.microsoft.com/v1.0/users \
-H "Authorization: Bearer <access_token>" \
-H "Content-Type: application/json" \
-d '{
  "accountEnabled": true,
  "displayName": "NewUser",
  "mailNickname": "newuser",
  "userPrincipalName": "newuser@victimdomain.com",
  "passwordProfile": {
    "forceChangePasswordNextSignIn": true,
    "password": "P@ssword123!"
  }
}'
```

Or:

```bash
bashCopyEdit# Assign admin role to compromised user
az ad user add-owner --id compromiseduser@victimdomain.com --owner-object-id <admin-role-id>
```

✅ **Result**: Adversary runs powerful commands through Azure APIs without needing direct shell access — pure cloud-native execution.

***

## 📊 **Execution Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique | MITRE ID  | Entra ID Example                                                            |
| ---------------------- | --------- | --------------------------------------------------------------------------- |
| Cloud API              | T1059.009 | Use Graph API / ARM API to create users, assign roles, manipulate directory |

***

## 🎯 Final Summary

Defending against Execution in Entra ID focuses on:

* **Monitoring API usage patterns (especially role modifications, user creations, service principal changes)**
* **Securing token access and restricting Graph/ARM API permissions**
* **Applying Conditional Access policies to control privileged actions**
* **Auditing all administrative operations in Entra ID logs**



