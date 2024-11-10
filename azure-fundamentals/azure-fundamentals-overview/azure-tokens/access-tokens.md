# Access Tokens

## **Access Tokens in Microsoft Entra ID**

Access tokens are like special digital keys that grant access to certain doors in a building. These doors represent specific services or data that a user or an application wants to access. They are mainly used in the Microsoft identity system to allow applications to securely access resources, like a web API, on behalf of a user.

### **Key Points About Access Tokens**:

1. **Purpose**: Access tokens authorize access to resources. They are different from ID tokens, which are only used to prove that a user is logged in.
2. **Claims**: The pieces of information within an access token that decide what it can do are called **claims**. Think of claims as the "permissions" written on the key that specify which doors it can open.
3. **Sensitive Nature**: Because access tokens can open specific "doors" (grant access to data), they are sensitive and must be kept secure to avoid misuse.

### **How Access Tokens Work**

* **Use by Clients**: When an application, called a **client**, wants to access a resource (like an API), it receives an access token.
* **Opaque Tokens**: For the client, the token is just a long string of letters and numbers—it doesn’t need to understand what’s inside. The application just uses it to prove it has permission.
* **Validation by the Resource**: The resource that receives the token (like the API) is the one that should read and validate it, to make sure it’s real and still valid.

### **Types of Access Tokens**

Microsoft provides two versions of access tokens:

* **v1.0**: This version is used by applications that are only connected to Microsoft’s business environment.
* **v2.0**: This version is used by applications that need to work with consumer accounts (like personal Microsoft accounts) in addition to business accounts.

The main difference between these versions is the format and what kind of information (claims) is inside the token.

### **Who Owns the Token?**

* **The Resource Owns It**: The "resource" (the data or service being accessed) owns the access token. It means that the resource is responsible for validating and using the token to decide if access should be granted.
* **Audience Claim (`aud`)**: The token has an `aud` (audience) claim that indicates which resource the token is intended for. Only the intended resource should accept the token.

### **How Long Do Tokens Last?**

* **Default Lifetime**: Access tokens usually last between **60 and 90 minutes**. This variability helps improve security by avoiding predictable patterns.
* **Custom Policies**: Organizations can change how long tokens last by using policies, but sometimes other security settings override these adjustments.

If the token expires, the application needs to use a **refresh token** to get a new one without having to prompt the user to log in again.

### **Validating Tokens**

Only certain types of applications need to validate tokens:

* **Web APIs**: If a web API receives a token from a client, it must validate it to make sure it’s valid.
* **Web Applications**: Web applications must validate **ID tokens** to make sure the person trying to log in is really who they say they are.

To validate a token, applications need to:

1. **Check the Signature**: Tokens have a special signature that proves they haven’t been tampered with. This is done using public keys.
2. **Verify the Audience**: Ensure the token is actually meant for the resource (API or service) that received it.

Microsoft provides tools and libraries (like **Microsoft.Identity.Web**) that can help developers easily perform these checks, especially if they’re using platforms like ASP.NET.

### **Single-Tenant vs. Multi-Tenant Applications**

* **Single-Tenant**: These are applications that work only within one organization’s directory. Tokens for these apps are validated against specific information unique to that organization.
* **Multi-Tenant**: These apps can work across many organizations. When validating tokens for multi-tenant applications, it’s important to ensure the token’s details match the expected organization.

### **Signing and Issuer Information**

Tokens are signed using a cryptographic key to make sure they are authentic:

* **Signature Verification**: The signature on the token helps verify that it hasn’t been altered. Microsoft regularly changes the keys used for signing, so applications need to stay updated.
* **Issuer (`iss`) Claim**: The `iss` (issuer) claim shows where the token came from. When validating, the application must make sure that this matches the expected source to prevent security risks.

### Claims Reference

{% embed url="https://learn.microsoft.com/en-us/entra/identity-platform/access-token-claims-reference" %}
