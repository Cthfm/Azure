# Create a Basic Policy

### **Hands-On Lab: Create a Basic DLP Policy**

**Objective:**\
Create a policy that prevents credit card numbers from being shared outside the organization.

#### Step 1: Create a DLP Policy

1. Open [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/).
2. Go to **Data Loss Prevention** → **Policies** → **+ Create Policy**.
3. Choose the **Financial Data** template.
4. Name your policy **Protect Credit Card Numbers**.

#### Step 2: Configure Rules

1. Set the **location** to **Exchange Online** and **OneDrive**.
2. Under **Rules**:
   * If content contains **Credit Card Numbers**,
   * And the recipient is **outside the organization**,
   * **Block** the action and **notify** the user with a policy tip.

#### Step 3: Review and Turn On

* Review your settings.
* Turn the policy **on**.
* Test by sending a fake credit card number to an external email address and see the policy tip in action.
