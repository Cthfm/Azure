# Refresh Tokens

## **Refresh Tokens in Azure Identity Platform**

A refresh token is used to obtain new access tokens when the current access token expires. It can also be used to get new tokens for other resources, allowing clients to maintain access without user reauthentication. Refresh tokens are linked to a user and client combination but aren't tied to a specific resource or tenant, enabling their use across multiple resources where permission is granted.

### **Token Lifetime**:

* Refresh tokens last longer than access tokens: typically 24 hours for single-page apps and 90 days for others.
* Each time a refresh token is used, it replaces itself, but old tokens aren't automatically revoked—meaning they should be deleted securely after use.
* Single-page apps need to renew their refresh tokens every 24 hours, as they expire after that period. This involves re-running the authorization flow, usually without user credential prompts.

### **Token Revocation and Security**:

* Refresh tokens can be revoked at any time due to password changes, administrative actions, or other security events.
* Security considerations: Refresh tokens must be securely stored and protected as they can be extracted if the device or application is compromised.
* Revocation: Tokens may be revoked by users, admins, or due to password resets, requiring reauthentication to obtain new tokens.
