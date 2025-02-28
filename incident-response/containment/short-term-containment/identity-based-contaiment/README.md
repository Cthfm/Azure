# Identity Based Contaiment

### **Identity & Access Containment**

#### **Disabling Compromised User Accounts**

**Method:** Utilize Entra ID to disable the user account via Portal

**Steps:**

1. Navigate to **Microsoft Entra ID** in the Azure portal.
2. Select **Users** and locate the compromised account.
3. Click **Block sign-in** under the **Manage** section.
4. Confirm the action to disable the account.

#### **Resetting Passwords & Enforcing MFA**

**Method:** Require users to reset passwords and enforce Multi-Factor Authentication (MFA) via portal

**Steps:**

1. Navigate to **Users** in Entra ID.
2. Select the compromised user and click **Reset password**.
3. Enforce MFA through **Security > Conditional Access > MFA policies**.

#### **Revoking Active Sessions**&#x20;

**Method:** Force user reauthentication via portal

**Steps:**

1. Go to Entra ID **Users**.
2. Select the user and click **Sign-in logs**.
3. Click **Revoke sessions**.

#### **Configuring Conditional Access Policies**

**Method:** Create Conditional Access policies based on risk signals.

**Steps:**

1. Navigate to **Conditional Access Policies**.
2. Create a new policy restricting access for high-risk sign-ins.
3. Apply policy enforcement.

