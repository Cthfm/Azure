# Azure Tokens

## T**oken Types in Azure Identity Platform and Defences**

For threat hunters, understanding tokens is vital for detecting unauthorized access, token abuse, and anomalies during authentication and authorization. Tokens provide insights into actions like misuse of privileges, replay attacks, and lateral movement. Proper analysis of token structure, claims, and validation helps identify OAuth or SSO abuse and attribute suspicious activity, ultimately enhancing security. As part of this section, we will also look at Continuous Access Evaluation (CAE).

### **Access Tokens:**

* **Purpose:** Authorization to access specific resources (e.g., APIs).
* **Format:** JWT (JSON Web Token).
* **Lifetime:** Short-lived (60-90 minutes).
* **Usage:** Grants access to resources.

### **ID Tokens:**

* **Purpose:** Authentication to prove the user's identity.
* **Format:** Always JWT.
* **Lifetime:** Valid for one hour.
* **Usage:** Issued after login to confirm user identity.

### **Refresh Tokens:**

* **Purpose:** Obtain new access tokens after expiration.
* **Format:** Not always JWT.
* **Lifetime:** Long-lived (days or more).
* **Usage:** Maintains user sessions without re-authentication.

### **Primary Refresh Tokens (PRTs):**

* **Purpose:** The PRT is a session token that provides access to cloud resources across devices. It's used by Azure AD to provide SSO across applications, even on different devices, without prompting users for credentials repeatedly.
* **Format:** The PRT itself is opaque to clients; it is encrypted and stored securely on the device.
* **Lifetime:** Long-lived; typically persists until the user signs out, changes their password, or the device is deemed untrusted. The PRT has a rolling expiration mechanism that keeps it valid as long as the device is healthy.
* **Usage:** Obtains new tokens (both access and ID tokens) for applications without requiring user re-authentication.

### Continuous Access Evaluation

* **Purpose:** Continuous Access Evaluation (CAE) enforces changes in user status or network conditions in near real-time. CAE improves security by instantly re-evaluating access policies rather than waiting for token expiration.
* **Usage:** CAE is used to provide real-time enforcement of security policies for Microsoft cloud services by immediately reacting to changes like user disablement or network shifts. It ensures that users lose or gain access promptly based on updated policies, rather than waiting for token expiration.

