# Identity Protection

## Identity Protection Overview

Microsoft Entra ID Protection helps organizations detect, investigate, and remediate identity-based risks using insights from a vast array of signals collected daily. These risks, such as anonymous IP usage, password spray attacks, and leaked credentials, are assessed during sign-ins, generating a risk level that informs Conditional Access policies or integration with security tools like SIEMs.&#x20;

Administrators can investigate risks through detailed reports on risky sign-ins and users, and remediation can be automated based on risk levels or handled manually through administrative review. Data from Identity Protection can be exported and integrated with other tools for extended analysis, archiving, and correlation, enhancing an organization's overall security posture.





### Role Requirements:

| Role                                                                                                                                              | Can do                                                                                                                      | Can't do                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [Security Administrator](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) | Full access to Identity Protection                                                                                          | Reset password for a user                                                                                                       |
| [Security Operator](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator)           | <p>View all Identity Protection reports and Overview<br><br>Dismiss user risk, confirm safe sign-in, confirm compromise</p> | <p>Configure or change policies<br><br>Reset password for a user<br><br>Configure alerts</p>                                    |
| [Security Reader](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader)               | View all Identity Protection reports and Overview                                                                           | <p>Configure or change policies<br><br>Reset password for a user<br><br>Configure alerts<br><br>Give feedback on detections</p> |
| [Global Reader](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader)                   | Read-only access to Identity Protection                                                                                     |                                                                                                                                 |
| [User Administrator](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator)         | Reset user passwords                                                                                                        |                                                                                                                                 |

\


### License requirements 

| Capability              | Details                                                                        | Microsoft Entra ID Free / Microsoft 365 Apps                                                            | Microsoft Entra ID P1                                                                                   | Microsoft Entra ID P2 |
| ----------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | --------------------- |
| Risk policies           | Sign-in and user risk policies (via Identity Protection or Conditional Access) | No                                                                                                      | No                                                                                                      | Yes                   |
| Security reports        | Overview                                                                       | No                                                                                                      | No                                                                                                      | Yes                   |
| Security reports        | Risky users                                                                    | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Full access           |
| Security reports        | Risky sign-ins                                                                 | Limited Information. No risk detail or risk level is shown.                                             | Limited Information. No risk detail or risk level is shown.                                             | Full access           |
| Security reports        | Risk detections                                                                | No                                                                                                      | Limited Information. No details drawer.                                                                 | Full access           |
| Notifications           | Users at risk detected alerts                                                  | No                                                                                                      | No                                                                                                      | Yes                   |
| Notifications           | Weekly digest                                                                  | No                                                                                                      | No                                                                                                      | Yes                   |
| MFA registration policy |                                                                                | No                                                                                                      | No                                                                                                      | Yes                   |
