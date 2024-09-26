# Conditional Access Session Control

## **What Are Session Controls?**

**Session Controls** in Conditional Access policies help organizations manage user behavior during an active session. These controls are useful when you want to allow access to a resource but want to enforce additional security or monitoring during that session.

Unlike **Grant Controls**, which determine whether access is allowed or blocked, **Session Controls** define what a user can do **after** access is granted. They work by integrating with Microsoft Defender for Cloud Apps to enforce real-time policies, limit actions, and monitor for suspicious activity.

### **Types of Session Controls**

There are three primary types of Session Controls that you can configure in Conditional Access:

1. **Monitor and Control with Conditional Access App Control**: This session control allows real-time monitoring of user activities within an app, such as restricting actions like downloading or copying files based on user context (e.g., device, location).
2. **Sign-in Frequency**: This session control defines how often users must reauthenticate within an active session, ensuring that long-running sessions are periodically verified.
3. **Persistent Browser Session**: This control determines whether users need to reauthenticate across multiple browser sessions or if their session should persist, even after closing the browser.

In this lesson, we’ll focus on **Conditional Access App Control**, which offers the most advanced session monitoring and restriction capabilities.

### **Introduction to Microsoft Defender for Cloud Apps**

**Microsoft Defender for Cloud Apps** (formerly known as Microsoft Cloud App Security) is a cloud access security broker (CASB) that provides comprehensive visibility, data controls, and threat protection across cloud apps. It integrates with Conditional Access to enforce real-time monitoring and control of user sessions.

When you configure Conditional Access App Control, Microsoft Defender for Cloud Apps allows you to:

* **Monitor user activity** within a cloud app.
* **Enforce restrictions** on specific actions (e.g., downloading, printing, or copying files).
* **Apply risk-based controls** during the session if abnormal behavior is detected.

This real-time monitoring is particularly useful for protecting sensitive data while allowing users to access apps and complete tasks.

### **How Conditional Access App Control Works**

Conditional Access App Control uses **reverse proxy** technology to monitor and control user actions within a session. When a session control policy is triggered, all user traffic is routed through Microsoft Defender for Cloud Apps, allowing it to inspect and control user activities in real time.

**Key Features:**

* **Session monitoring**: Monitor all activities a user performs within a session, including file access, downloads, uploads, and sharing.
* **Activity restrictions**: Restrict specific actions within a session, such as preventing downloads or printing when a user is on an unmanaged or non-compliant device.
* **Session alerts**: Configure alerts for risky or suspicious behavior, such as a user attempting to access sensitive data from an unusual location or downloading large volumes of files.

### **Best Practices for Using Session Controls**

**1. Start with Monitor-Only Mode:**

* Always begin with **Monitor-only mode** before fully enforcing session restrictions. This helps you understand how users interact with apps and identify any potential disruptions.

**2. Apply Session Controls to High-Risk Scenarios:**

* Focus on applying session controls to high-risk situations, such as users accessing apps from unmanaged devices or external networks.

**3. Use Conditional Access Logs:**

* Regularly review logs in **Microsoft Defender for Cloud Apps** to track user behavior and fine-tune policies based on observed activities.

**4. Balance Security and Usability:**

* While session controls are powerful, it’s important to avoid over-restricting users. Make sure that your policies are aligned with business needs and don’t disrupt productivity.
