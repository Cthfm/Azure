# Identity Provider Matrix (Entra ID)

## Overview

The Identity Provider Matrix in the MITRE ATT\&CK framework is an extension focusing on tactics, techniques, and procedures (TTPs) related to identity providers (IdPs) and how attackers might target these environments to compromise identity and access management (IAM). This matrix captures specific attack vectors within cloud-based and traditional identity systems, such as Microsoft Entra ID, Okta, Ping Identity, and others. For this scope of this manual, we will focus on Entra ID only.

### Key Elements of the Identity Provider Matrix

1. **Tactics and Techniques**: It covers various phases of an attack, similar to the traditional ATT\&CK matrix, such as initial access, persistence, privilege escalation, defense evasion, credential access, and more.
2. **Attack Scenarios**: The matrix emphasizes scenarios unique to identity providers, such as:
   * **Account Manipulation**: Targeting accounts, roles, and permissions within IdPs to gain unauthorized access.
   * **Authentication Mechanism Abuse**: Exploiting or bypassing multi-factor authentication (MFA), password policies, and federation mechanisms.
   * **Credential Access**: Techniques to capture or abuse credentials stored in the IdP environment, like token theft or session hijacking.
3. **Cloud and Hybrid Environments**: It addresses both cloud-native and hybrid identity models where organizations might have federated or synchronized identities between on-premises and cloud.
4. **Defensive Recommendations**: The Identity Provider Matrix also includes mitigations specific to IAM controls, MFA, conditional access, logging, and monitoring practices.

### Usage in Security Programs

The Identity Provider Matrix is invaluable for:

* **Threat Hunting and Incident Response**: It helps focus on monitoring identity-based threats across the access lifecycle.
* **Red Team Exercises**: It can assist in simulating attacks that test identity and access resilience within IdPs.
* **Training and Awareness**: Security teams use the matrix to train on specific IdP-related risks and to build an understanding of modern identity-focused attacks.

