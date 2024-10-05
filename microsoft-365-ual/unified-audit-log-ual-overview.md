# Unified Audit Log (UAL) Overview

The **Unified Audit Log (UAL)** in **Microsoft 365** is a centralized log that captures activity from various Microsoft services, such as **Exchange Online, SharePoint Online, OneDrive, Teams**, and **Azure Active Directory**. It allows administrators to track user and admin activities across these services, which is essential for security, compliance, and auditing purposes.

Key points about the Unified Audit Log:

1. **Activities Captured:**
   * User activities: File accesses, sharing actions, mailbox access, etc.
   * Administrator actions: Changes to configurations, user permissions, mailbox delegations, and more.
   * Security events: Login attempts, policy changes, and data access events.
2. **Services Logged:**
   * **Exchange Online:** Logs mailbox access, email send/receive, and changes in mailbox permissions.
   * **SharePoint Online and OneDrive for Business:** Logs file access, sharing, and file modifications.
   * **Teams:** Logs actions like adding/removing team members, meeting creation, etc.
   * **Azure Active Directory:** Logs user and admin sign-in activities, role changes, and group modifications.
3. **Accessing the UAL:**
   * UAL can be accessed from the **Microsoft Purview Compliance Center** under the **Audit** section.
   * You can search logs for specific users, activities, and time frames to investigate incidents.
4. **Retention:**
   * The default retention period for audit logs is 90 days, but this can be extended for organizations with certain Microsoft 365 plans (such as E5) or through **Advanced Audit** capabilities, which allow logs to be retained for up to 1 year or more.
5. **Use Cases for Security:**
   * **Investigating breaches or suspicious behavior** by tracking login attempts or unusual access patterns.
   * **Compliance auditing** to ensure that user actions align with organizational policies.
   * **Forensics and incident response**, by correlating logs to investigate the timeline and scope of security incidents.
