# Continuous Access Evaluation (CAE)

## Overview

Continuous Access Evaluation (CAE) is a modern security enhancement provided by Microsoft Entra (previously Azure Active Directory) that enables real-time evaluation of access conditions, ensuring a more responsive and dynamic enforcement of security policies for users. Instead of relying solely on access token expiration and refresh cycles, CAE allows immediate re-evaluation of access in response to changes such as user status or network conditions. This results in improved security, user experience, and overall reliability of access control mechanisms.

### Tokens Background

Tokens used in cloud applications are typically valid for one hour by default. When they expire, the client application refreshes them by contacting Microsoft Entra. This refresh process presents an opportunity to re-evaluate security policies for user access. For example, if a Conditional Access policy or other changes affect a user's access, Microsoft Entra may decide not to refresh the access token. This could occur if a user is disabled, marked as high-risk, or when their status changes according to the organization's Conditional Access policies.

### CAE's Value

CAE makes it possible to enhance security and responsiveness by allowing proactive communication between the token issuer (Microsoft Entra) and the application (e.g., Exchange, SharePoint, Teams). Instead of waiting for a token to expire, CAE ensures that policies are evaluated in real time, leading to faster responses to policy violations or changes in user conditions. It leverages the OpenID Continuous Access Evaluation Profile (CAEP) standard to achieve this goal.

### **Key Features of CAE**

**Real-Time Enforcement of Security Policies:**

* CAE enables policy violations or significant security changes to be enforced almost immediately—typically within a latency of up to 15 minutes. This means that if a user's risk status changes, if they are disabled, or if their network location changes, CAE allows rapid enforcement of access policies without waiting for token expiration.

**Critical Event Evaluation and Conditional Access Policies:**

* **Critical Event Evaluation**: Specific events like account disablement, password reset, or elevated risk detection can be instantly detected and acted upon. Microsoft Entra sends signals to the services to revoke user access in near real-time when critical events occur.
* **Conditional Access Policy Evaluation**: In addition to critical events, CAE enforces Conditional Access policies, such as location-based policies. For instance, if a user moves to an unauthorized IP address or network, CAE enforces the network policy immediately.

**Claim Challenge Mechanism:**

* CAE introduces a "claim challenge" mechanism for clients. Typically, clients cache access tokens until they expire. With CAE, resource providers (such as Exchange, Teams, or SharePoint) may reject tokens even if they have not yet expired. The claim challenge prompts the client to bypass its cached token and request a new token from Microsoft Entra, ensuring that all conditions are re-evaluated for ongoing compliance.

**Token Lifetime Modifications:**

* Traditional token expiration policies are supplemented with CAE, allowing access tokens to become long-lived (up to 28 hours) if continuous access evaluation is in place. In CAE sessions, revocation events and policy evaluations become the primary mechanisms for enforcing access changes, rather than relying solely on arbitrary token expiry. For non-CAE clients, the default access token lifetime remains one hour unless changed through specific token lifetime configurations.

**Client Capabilities for CAE:**

* CAE requires specific client-side capabilities to handle claim challenges effectively. For instance, applications like Outlook, Teams, OneDrive, and Office on various platforms (web, Win32, iOS, Android, and Mac) need updates to properly understand and respond to claim challenges. This allows these applications to maintain CAE-aware sessions and stay compliant with real-time security requirements.

### **Scenarios and Benefits**

CAE brings significant benefits to organizations by improving how access policies are evaluated and enforced. There are two major scenarios where CAE plays a vital role:

1. **Critical Event Evaluation:**
   * In this scenario, applications such as Exchange Online, SharePoint Online, and Teams subscribe to critical Microsoft Entra events. When a critical event occurs, such as an account being disabled or a password being reset, these events are instantly evaluated, and user access is revoked as needed.
   * Events monitored by CAE for critical evaluation include:
     * User account is deleted or disabled.
     * User password is changed or reset.
     * Multifactor authentication (MFA) is enabled for the user.
     * Administrator explicitly revokes all refresh tokens for a user.
     * High user risk detected by Microsoft Entra Identity Protection.
   * With critical event evaluation, users will lose access to resources (e.g., SharePoint Online files, Teams communications, Exchange emails) within minutes of such an event, ensuring that security risks are quickly mitigated.
2. **Conditional Access Policy Evaluation:**
   * Applications such as Exchange Online, Teams, and Microsoft Graph are capable of synchronizing key Conditional Access policies directly within the service itself. This allows near real-time enforcement of Conditional Access policies, such as location restrictions, and immediate action when network conditions change.
   * For example, if a user moves outside an allowed IP range, CAE enforces the policy immediately, ensuring the user loses access promptly.

### **Benefits of Real-Time Enforcement:**

* **User Account Termination or Password Change**: When a user account is disabled or the password is reset, the user's session is revoked in near real time.
* **Network Location Change**: CAE allows Conditional Access policies to be enforced in real time. If a user changes to a network that is not in the approved list, they lose access immediately.
* **Protection from Token Export**: With CAE, Conditional Access location policies prevent access tokens from being used on untrusted devices or networks, protecting against unauthorized token export.

### **Client Capabilities and Claim Challenges**

Before CAE, applications used cached access tokens until they expired. With CAE, clients must be able to handle situations where a token is rejected before its expiry time. To address this, Microsoft introduced a "claim challenge" mechanism.

**How Claim Challenges Work:**

* If the resource provider detects that access should no longer be granted (e.g., due to changes in network location or user risk), it rejects the token and sends a "claim challenge" response to the client.
* The CAE-aware client recognizes the claim challenge and bypasses its cached token, requesting a fresh token from Microsoft Entra. This ensures that any changes in policy or user status are taken into account before granting further access.

The latest versions of applications like Outlook, Teams, and OneDrive are updated to support claim challenges, which ensures compliance with CAE and enables continuous enforcement of policies without user disruption.

### **Token Lifetime and Session Management**

With CAE, access tokens become long-lived—up to 28 hours—if the session is CAE-aware. This means that the access control relies primarily on real-time evaluations rather than short token lifetimes. Applications benefit from increased session stability without compromising on security, as any critical event or policy change will still trigger immediate revocation.

Non-CAE clients, on the other hand, continue to use the default one-hour token lifetime unless explicitly configured otherwise.

## **Network Configuration Considerations and Limitations**

CAE uses IP-based named locations to enforce location policies. However, modern network topologies often introduce variability in source IP addresses, which can affect Conditional Access enforcement. For instance, environments that use load balancers, split tunneling, or shared proxy IP addresses can present different IP addresses to Microsoft Entra versus the resource provider, complicating policy enforcement.

In some complex scenarios, Microsoft Entra may grant temporary access based on previous IP address information, issuing a one-hour token that suspends IP address checks until token expiration. Administrators can opt to disable this exception by using "Strict Location Enforcement," available as a public preview.

Additionally, CAE does not support enforcing policies in real-time for guest user accounts. Guest users are not subject to CAE revocation events or instant IP-based Conditional Access policy enforcement, which can present a limitation for organizations with guest collaborations.

### **Migration to Conditional Access and CAE Configuration**

Previously, CAE settings were configured under Security. However, to streamline management, CAE settings are now part of Conditional Access policies. Existing customers may need to migrate their CAE configurations to take full advantage of CAE directly within Conditional Access policies. This ensures that CAE is consistently applied across all users and policies, improving overall policy management and enforcement.

### **Summary**

Continuous Access Evaluation (CAE) significantly enhances the security of Microsoft cloud environments by enabling real-time enforcement of user policies and access conditions. With CAE, organizations can benefit from faster enforcement of changes, improved responsiveness to user events (like account disablement), and greater control over Conditional Access policies.

By adopting CAE, organizations can:

* **Respond Faster** to user account changes, policy violations, and security risks.
* **Improve User Experience** by extending session stability without compromising security.
* **Ensure Compliance** with organizational policies, such as network location-based restrictions, almost instantaneously.
