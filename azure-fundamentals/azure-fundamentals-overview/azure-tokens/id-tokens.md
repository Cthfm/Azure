# ID Tokens

**What are ID Tokens?**

ID tokens are proof that a user is authenticated, like a digital ID badge. They help client applications verify that the user is who they claim to be. Unlike access tokens (used for authorization), ID tokens confirm user identity.

### **Key Characteristics**

* **Format**: ID tokens are always in JSON Web Token (JWT) format and contain **claims** (pieces of information about the user).
* **Versions**: There are **v1.0** and **v2.0** versions of ID tokens, which vary based on the endpoint used:
  * **v1.0**: Used for older or single-tenant applications.
  * **v2.0**: Recommended for new applications, supports more scenarios.

### **Token Lifetime**

* By default, ID tokens last **one hour**.
* After expiry, the client must request a new token to continue using the application.

### **Validating ID Tokens**

* Only **confidential clients** (e.g., server-side apps) should validate ID tokens.
* The validation process involves:
  * Checking the **signature** to ensure the token hasn't been tampered with.
  * Verifying the **issuer** to confirm it was issued by the right authority.
* There are many **libraries** available to simplify token validation—using these is recommended over implementing your own.

### **Claims to Validate**

* **Timestamps** (`iat`, `nbf`, `exp`): Ensure the token is used within its valid time.
* **Audience** (`aud`): Should match your app’s ID.
* **Nonce**: Must match the original request to prevent replay attacks.

### Endpoints

* v1.0: https://login.microsoftonline.com/common/oauth2/authorize
* v2.0: https://login.microsoftonline.com/common/oauth2/v2.0/authorize

### Claim Reference

{% embed url="https://learn.microsoft.com/en-us/entra/identity-platform/id-token-claims-reference" %}
