# Best Practices for Conditional Access

## **Best Practices for Creating Conditional Access Policies**

### **1. Test Policies in Report-Only Mode First**

Before fully enabling any policy, start in **Report-only mode**. This allows you to see how the policy will behave without enforcing it, preventing disruptions to user access.

### **2. Exclude Break-Glass Accounts**

Always exclude at least one emergency account (often called a break-glass account) from Conditional Access policies. This ensures administrators can access the environment in case of a misconfiguration or emergency.

### **3. Target Specific Groups for Early Testing**

Instead of applying a new policy to all users right away, test the policy with a small group of users first. Once you verify that the policy works as expected, you can roll it out to larger groups.

### **4. Layer Policies for Maximum Security**

Apply multiple Conditional Access policies for different user groups, applications, and access scenarios to create layered security. For example, apply stricter policies to high-privilege accounts like Global Administrators.

### **5. Review and Update Policies Regularly**

Conditional Access policies should be reviewed periodically to ensure they align with the organization's evolving security needs and compliance requirements.
