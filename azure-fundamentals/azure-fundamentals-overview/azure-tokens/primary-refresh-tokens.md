# Primary Refresh Tokens

### **Primary Refresh Token (PRT) Overview**

A Primary Refresh Token (PRT) is an essential authentication artifact used in the Microsoft Entra ID to enable Single Sign-On (SSO) across applications and services on a user's device. It is a JSON Web Token (JWT) that serves as a foundational component to streamline user authentication, reduce repeated login prompts, and provide secure access to multiple applications without requiring users to reauthenticate frequently.

PRTs are designed for Windows 10 and later, Windows Server 2016 and later, as well as iOS and Android devices. These tokens are fundamental for creating a seamless and secure experience for users accessing different apps and services using the same device.

### **Key Concepts and Components of a PRT**

PRTs function in conjunction with several key components in the Microsoft Entra ID ecosystem, especially on Windows devices:

* **Cloud Authentication Provider (CloudAP)**: This component handles the authentication for Windows logins, verifying user credentials during sign-in. It facilitates the issuance of a PRT by working with Microsoft Entra ID.
* **Web Account Manager (WAM)**: Acts as a token broker on Windows, helping obtain tokens for apps and enabling SSO. It provides a standardized way for apps to interact with identity providers.
* **Trusted Platform Module (TPM)**: A hardware component that provides additional security for user and device secrets. It secures cryptographic keys, which are used to protect PRTs from being stolen or tampered with.
* **Microsoft Entra CloudAP Plugin** and **WAM Plugin**: These plugins interface with CloudAP and WAM to ensure SSO experiences for Microsoft Entra authenticated devices. They verify credentials, issue PRTs, and facilitate token renewals and requests for apps.

### **What Does a PRT Contain?**

A PRT includes:

* **Device ID**: This identifies the specific device to which the PRT is tied. It helps Microsoft Entra ID determine the state of the device, such as whether it complies with organizational policies.
* **Session Key**: A symmetric key used as proof of possession, ensuring that any token request made using a PRT comes from the original device. This key is encrypted and bound to the device to prevent unauthorized use.

The PRT is a secure and opaque token, meaning that its contents are not accessible to client components and are only readable by Microsoft Entra ID.

### **How is a PRT Issued?**

A PRT is issued during **device registration** and **user authentication** under specific conditions:

* **Device Registration**: Devices must be registered with Microsoft Entra ID to obtain a PRT. During registration, the **dsreg** component generates cryptographic key pairs (Device Key and Transport Key), which are bound to the device's TPM.
* **PRT Issuance**:
  * **Microsoft Entra Joined or Hybrid Joined Devices**: A PRT is issued during Windows login when users sign in with their organization credentials, such as passwords or **Windows Hello for Business**.
  * **Microsoft Entra Registered Devices**: A PRT can be issued when a user adds a secondary work account to their Windows device. The issuance happens through settings or prompts from apps like Outlook.

In these scenarios, the **Microsoft Entra CloudAP plugin** is responsible for communicating with Microsoft Entra ID to authenticate the user and issue a PRT.

### **PRT Lifetime and Renewal**

* **Lifetime**:
  * A PRT is typically valid for **14 days**.
  * The validity is continually extended as long as the user keeps using the device, which prevents frequent reauthentication.
* **Renewal**:
  * **CloudAP Plugin Renewal**: The PRT is renewed every **4 hours** by the CloudAP plugin as part of regular Windows sign-in activity.
  * **WAM Plugin Renewal**: The **WAM plugin** can also renew the PRT while processing token requests for applications. If a refresh token is unavailable, WAM uses the PRT to obtain a new access token and refresh token, which also renews the PRT.

### **How is a PRT Used?**

A PRT enables **Single Sign-On (SSO)** across all applications on the user's device, facilitating seamless authentication without repeated prompts:

* **Microsoft Entra CloudAP Plugin**: During user sign-in to Windows, the CloudAP plugin uses the PRT to authenticate the user and cache the PRT for subsequent sign-ins, even in offline scenarios.
* **Microsoft Entra WAM Plugin**: When a user accesses applications or web resources, the WAM plugin uses the PRT to request necessary access or refresh tokens, enabling SSO. For web applications, the WAM plugin injects the PRT into the browser, enabling automatic authentication.

### **PRT Protection Mechanisms**

The security of a PRT is primarily handled by binding it to the device:

* **TPM Binding**: During device registration, cryptographic keys are generated, and the **private keys** are stored securely in the TPM. The TPM acts as a hardware vault, ensuring that the keys used to secure the PRT cannot be extracted or tampered with.
* **Proof of Possession (Session Key)**: When a PRT is issued, Microsoft Entra ID provides an encrypted **session key**, which acts as proof of possession. This key is encrypted with the **Transport Key** and can only be decrypted by the TPM. This mechanism ensures that any token requests made using a PRT are signed by the correct session key and cannot be used from any other device.

### **Multi-Factor Authentication (MFA) and PRT**

* When users sign in using Windows Hello for Business, the PRT issued contains an MFA claim. This means that applications relying on the PRT do not need additional MFA prompts, providing a smoother user experience.
* MFA can also be triggered during token requests through WAM if additional verification is required, and the renewed PRT will carry this MFA claim.

### **PRT Invalidation Scenarios**

A PRT can be invalidated for several reasons:

* **User or Device Disabled**: If the user or device is disabled in Microsoft Entra ID, the corresponding PRT is invalidated.
* **Password Change**: If a user changes their password, the PRT obtained using the old password is invalidated. Upon the next login, a new PRT is issued.
* **TPM Issues**: If the TPM fails, the PRT cannot be renewed. The device must go through a **re-registration** process to generate new cryptographic keys and obtain a new PRT.

### **PRT Usage During App Token Requests**

* When an application, like Outlook, requires an access token, the WAM plugin uses the PRT to request the token.
* The WAM plugin signs these requests with the **session key**, ensuring that Microsoft Entra ID can validate the origin and integrity of the request.
* If successful, Microsoft Entra ID issues an **access token** and a **refresh token**, encrypted with the session key, which are securely managed by the WAM plugin.

### **PRT and Browser SSO**

* **Browser Single Sign-On**: When a user opens a browser and navigates to a Microsoft Entra login page, the PRT is used to authenticate the user seamlessly.
* The **CloudAP plugin** creates a PRT cookie signed with the session key, which is sent back to the browser for authentication purposes. This approach binds the cookie to the device and prevents unauthorized replay attacks.

### **PRT and Security Considerations**

* PRT is a **sensitive artifact** and must be protected rigorously. It is critical to bind the PRT to the TPM to ensure that it cannot be extracted from the device or reused elsewhere.
* Microsoft Entra Conditional Access policies are not evaluated when issuing or renewing a PRT, so security at the device level must be ensured.
* **TPM 2.0** is recommended for all Microsoft Entra devices to enhance the security of PRTs. TPM 1.2 is not used for PRT protection due to reliability concerns.

### **PRT Renewal and MFA Claims**

* **MFA During Sign-In**: If users log in with Windows Hello for Business or if MFA is required during WAM token requests, the renewed PRT will contain an MFA claim, extending the MFA validity without prompting users multiple times.
* **Partitioned PRTs**: Windows maintains separate PRTs for different credential types (e.g., password, Windows Hello, smart card). Each PRT contains specific claims related to the credential used, keeping MFA claims isolated.
