# Sign-In Risk and Identity Protection

## **What is Sign-in Risk?**

**Sign-in risk** refers to the likelihood that a sign-in attempt is fraudulent or that the user’s credentials have been compromised. Azure Active Directory (Azure AD) uses machine learning and various signals to assess the risk of every sign-in and categorizes it into **low**, **medium**, or **high** risk levels.

Azure AD evaluates the risk based on:

* **User behavior**: Unusual activities such as sign-ins from unexpected locations or devices.
* **Known compromised credentials**: Credentials that have been exposed in breaches or phishing attempts.
* **Sign-in patterns**: Patterns that don’t match the user's regular behavior, like simultaneous logins from multiple regions.

By integrating this risk evaluation into Conditional Access policies, organizations can dynamically adjust security measures based on the assessed risk, enhancing protection without overburdening users.

## **Azure AD Identity Protection**

**Azure AD Identity Protection** is a feature that helps organizations detect, investigate, and respond to potential identity risks. It leverages Microsoft's vast threat intelligence network and machine learning to assess the risk level of user accounts and sign-in attempts.

**Key Features of Identity Protection:**

* **Risk detection**: Identifies anomalies that indicate suspicious activity.
* **Risk remediation**: Allows Conditional Access to trigger actions like requiring MFA or a password reset based on the sign-in risk.
* **Reporting**: Provides insights into risky sign-ins and compromised accounts through reports and dashboards in the Azure portal.

Identity Protection works in conjunction with Conditional Access to enforce risk-based access policies.

### **Types of Sign-in Risk**

Azure AD Identity Protection evaluates multiple risk signals to determine the level of risk associated with a sign-in attempt. These signals include:

**1. Atypical Travel:**

Occurs when a user signs in from a location that is not consistent with their typical behavior. For example, if a user signs in from New York and a few minutes later from Tokyo, Azure AD detects this as a sign-in risk because it is unlikely the user could travel that fast.

**2. Anonymous IP Address:**

If a sign-in attempt is made using an anonymous proxy or TOR network, Azure AD flags the sign-in as risky. This behavior is often associated with attempts to hide the origin of the sign-in and may indicate a fraudulent attempt.

**3. Unfamiliar Sign-in Properties:**

Azure AD detects sign-ins from devices, browsers, or IP addresses that the user hasn’t used before. Even if the location seems familiar, unfamiliar devices or browsers can trigger a medium or high sign-in risk.

**4. Malware-linked IP Address:**

This occurs when a sign-in attempt is made from an IP address that is known to be associated with malware or botnet activity.

**5. Leaked Credentials:**

If Microsoft detects that a user’s credentials have been exposed in a breach or phishing attack, Identity Protection flags the user’s account as high risk and triggers appropriate actions like a forced password reset.

### **Sign-in Risk Levels**

Azure AD categorizes sign-in risk into three levels:

**1. Low Risk:**

* No unusual behavior or anomalies detected.
* Typically considered a normal, expected sign-in attempt.

**2. Medium Risk:**

* Moderate suspicion that the account might be compromised.
* Example: A sign-in from an unfamiliar location but with no other strong indicators of compromise.

**3. High Risk:**

* High likelihood that the sign-in attempt is fraudulent or that the account is compromised.
* Example: A sign-in from a known malware-linked IP address or from a location with a history of malicious activity.

### **Integrating Sign-in Risk with Conditional Access**

Sign-in risk is a powerful condition that can be used to dynamically enforce access controls. By combining Conditional Access with Azure AD Identity Protection, you can automate actions based on the risk level of the sign-in.

**Example Policy Configuration:**

* **Low Risk**: Allow access without additional controls.
* **Medium Risk**: Require Multi-Factor Authentication (MFA) to confirm the user’s identity.
* **High Risk**: Block access entirely or require the user to reset their password before gaining access.

**How to Configure Sign-in Risk in Conditional Access:**

1. **Navigate to Conditional Access**: In the Azure AD portal, go to **Security** > **Conditional Access**.
2. **Create or Modify a Policy**: Select a policy to edit or create a new one.
3. **Configure Conditions**: Under **Conditions**, select **Sign-in risk**.
4. **Set the Risk Level**: Choose whether to apply the policy for low, medium, or high-risk sign-ins.
5. **Define Controls**: In the **Grant** section, choose the appropriate actions based on the risk level (e.g., require MFA, block access, or require a password reset).
6. **Enable and Monitor**: Enable the policy and monitor its impact using sign-in logs and Identity Protection reports.

### **Best Practices for Using Sign-in Risk**

**1. Prioritize High-Risk Sign-ins:**

* Implement stringent controls (like blocking access or requiring password resets) for high-risk sign-ins to prevent compromised accounts from being exploited.

**2. Require MFA for Medium Risk:**

* Use MFA for medium-risk sign-ins to ensure that users can verify their identity even if some risk factors are present.

**3. Regularly Review Risk Reports:**

* Leverage Identity Protection reports to monitor patterns in risky sign-ins, compromised accounts, and trends over time. This allows you to adjust your policies based on emerging threats.

**4. Educate Users:**

* Inform users about potential risks and how they can help protect their accounts, especially regarding password hygiene and recognizing phishing attempts. Encouraging users to register for MFA early can also prevent disruptions when policies are enforced.
