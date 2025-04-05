# Name Locations IP Location

## **What Are Named Locations?**

**Named Locations** in Azure Entra ID Conditional Access policies allow organizations to define specific geographic regions or network IP ranges that can be used to enforce access controls. These locations are typically categorized as either trusted or untrusted and can influence how Conditional Access policies are applied.

Named Locations allow you to:

* Define trusted corporate networks based on IP addresses.
* Restrict or allow access from specific countries or regions.
* Trigger additional security measures (such as MFA) when users attempt to access resources from untrusted or unfamiliar locations.

Using Named Locations enhances security by ensuring that users accessing critical resources are doing so from safe, known locations.

### **Types of Named Locations**

There are two main types of Named Locations that can be configured in Conditional Access:

**1. IP Address Ranges:**

These are specific IP addresses or IP ranges that are associated with trusted networks, such as corporate offices, VPNs, or specific third-party service providers.

**2. Country or Region-Based Locations:**

These locations are based on the geographic location from which a user is signing in. Azure Entra ID detects the user’s location based on their IP address and determines the associated country or region.

### **Best Practices for Using Named Locations**

**1. Regularly Update Trusted IP Ranges:**

Ensure that you keep your Named Locations up to date, especially when your organization adds new offices, VPNs, or changes its network infrastructure.

**2. Use MFA for Untrusted Locations:**

While allowing access from trusted locations without MFA can improve user experience, always enforce MFA for sign-ins from untrusted locations to reduce the risk of unauthorized access.

**3. Be Cautious When Blocking Entire Regions:**

Blocking entire countries or regions should be done carefully. If your organization operates globally, blocking access from certain regions might inadvertently prevent legitimate users from accessing services.

**4. Monitor Location-Based Sign-in Logs:**

Leverage Azure AD’s **Sign-in logs** to monitor where users are signing in from. This helps you detect suspicious or unexpected access attempts and refine your Named Location policies.
