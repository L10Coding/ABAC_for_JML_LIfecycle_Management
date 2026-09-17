# 🔎 Attribute-Based Access Controls (ABAC) for Joiner-Mover-Leaver (JML) Identity Lifecycle Management

**Platform:** Microsoft Entra ID  
**Focus:** Identity Lifecycle Management (ILM), Automation, Dynamic Groups, Enterprise App Access, Conditional Access (CA)**

# 👔 Executive Summary
In modern enterprise environments, managing user access manually creates operational bottlenecks and severe security vulnerabilities. This project demonstrates a fully automated Joiner-Mover-Leaver (JML) identity lifecycle built in Microsoft Entra ID using Attribute-Based Access Control (ABAC).

By leveraging core user attributes (such as Department and Job Title) as a dynamic source of truth, this architecture eliminates the need for manual administrative tickets. It automatically provisions resources for new hires, realigns security boundaries during internal role changes, and enforces instant access revocation during offboarding. The entire lifecycle is wrapped in context-aware Conditional Access (CA) policies to ensure a zero-trust security posture.

# 🚀 Key Takeaways & Business Impact
- Zero-Touch Provisioning: Reduced administrative overhead by automating group memberships and application assignments.
- Elimination of Access Creep: Solved a major compliance issue by ensuring users automatically lose old privileges when changing roles.
- Instant Risk Mitigation: Secured corporate data by verifying that disabled "Leaver" accounts are immediately blocked from all enterprise resources.
- Audit-Ready Infrastructure: Validated every identity lifecycle transition using Entra ID Sign-In and Audit logs to prove compliance.

## 📘 Project Overview

This project showcases use of **Attribute Based Access Controls (ABAC)** to implement a Joiner, Mover, Leaver (JML) lifecycle for employees at Indigo Blue Technology. 
**ABAC's** are utilized to automatically control: Group Membership, Access to Applications, Enforcement of Conditional Access policies, and Revoking Access for applicable staff members. Tasks were confirmed using Group Membership and Sign-In logs.


##   Adding Users to the environment

I created three users: Adam Brown, Jason Jones and Michelle Smith

| User | Department | Job Title |
|-----|------------|-----------|
| Adam Brown | Marketing | Content Strategist
| Jason Jones | Sales | Sales Analyst |
| Michelle Smith | Human Resources | Human Resources Analyst |

##   Confirmations
First User:
<img width="1000" height="800" alt="User Adam Brown confirmation" src="images/Adam Brown - Properties.jpg"/> 

Second User:
<img width="1000" height="800" alt="User Jason Jones confirmation" src="images/Jason Jones - Properties.jpg"/> 

Third User:
<img width="1000" height="800" alt="User Michelle Smith confirmation" src="images/Michelle Smith - Properties.jpg"/> 


##  📝 Creating Dynamic Security Groups

Created Dynamic Groups that will assign membership according to the user's attributes (Job Title):

<img width="1000" height="800" alt="Dynamic Group Creation - Marketing" src="images/Dynamic Group Creation - Marketing.jpg"/> 


**Confirmation of Dynamic Groups created for each department:**

<img width="1000" height="800" alt="Dynamic Group List" src="images/Dynamic Groups List.png"/> 


**Policy ran correctly, and now shows the users as members of their respective Dynamic Group:**

<img width="1000" height="800" alt="Dynamic Group Membership - HR" src="images/Dynamic Group Membership - HR.png"/> 

<img width="1000" height="800" alt="Dynamic Group Membership - Sales" src="images/Dynamic Group Membership - Sales.png"/> 

<img width="1000" height="800" alt="Dynamic Group Membership - Marketing" src="images/Dynamic Group Membership - Marketing.jpg"/> 


## 🔧 Created an Enterprise App (CA-Policy-Test-App):

- Configured access to `CA-Policy-Test-App` to require assignment, and then added two of my Dynamic Groups. This ensures access to the application is based on attributes of users.
- Configured SSO and SAML for users to access utilizing their Entra ID credentials.

<img width="1000" height="800" alt="Policy-Test App Configuration" src="images/CA-CA Policy Test App - Properties.png "/> 

<img width="1000" height="800" alt="Policy-Test App Assigned Groups" src="images/CA-CA Policy Test App - Applicable Groups.png "/> 


## 🔐 Establishing Conditional Access Policies according to Dynamic Group/Department

| Group | Controls |
|------|----------|
| Marketing | Require MFA |
| Sales | Session Controls |

<img width="1000" height="800" alt="Policy-Test App - Marketing" src="images/CA - CA Policy Test App  - Configuration - Marketing.png"/> 

<img width="1000" height="800" alt="Policy-Test App - Targeted Resources" src="images/CA - CA Policy Test App - Marketing - Targeted Resources.png"/> 

<img width="1000" height="800" alt="Policy-Test App - MFA Requirement" src="images/CA - CA Policy Test App - Marketing - MFA.png"/> 

<img width="1000" height="800" alt="Policy-Test App - Sales" src="images/CA - CA Policy Test App - Sales - Selected Group.png"/> 

<img width="1000" height="800" alt="Policy-Test App - Targeted Resources" src="images/CA - CA Policy Test App - Sales - Targeted Resource.png"/> 

<img width="1000" height="800" alt="Policy-Test App - Session Control" src="images/CA - CA Policy Test App - Sales - Session Control.png"/> 


## 📘 Joiner of J-M-L:

User `Jason Jones` signing in:
- User was prompted to update their password upon signing-in for the first time
- User was prompted to utilize MS Authenticator and was able to successfully enroll.
- Access to `CA-Policy-Test-App` confirmed via `Sign-In` and `Audit` logs
- Sign-In Activity logs confirmed the `Conditional Access Policy` was triggered and user successfully met the requirement, and the Conditional Access policy for the Marketing team was not applied to this member of the Sales team.

<img width="1000" height="800" alt="User Sign-In password prompt" src="images/User Sign-In - Jason  - Password Prompt.png"/> 

<img width="1000" height="800" alt="User Sign-In Authenticator Added" src="images/User Sign-In - Authenticator Added.png"/> 

<img width="1000" height="800" alt="User Sign-In Audit Logs Confirmation" src="images/App Audit Logs - Jason Jones.png"/> 

<img width="1000" height="800" alt="User Sign-In Audit Logs Confirmation" src="images/App Sign-In Activity Details - Jason Jones.png"/> 


## 📘 Mover of J-M-L:

User `Adam Brown` is moving to a new department:
- User's profile attributes were updated to reflect new department (Marketing -> Sales)
- No longer can access `Marketing` resources
- Now able to access `Sales` resources
- Access to `CA-Policy-Test-App` remains, and the `Conditional Access policy` established for the `Sales` team now applies.
- Automated process allows for RBAC to be implemented.

<img width="1000" height="800" alt="Updating user properties" src="Mover - Updating Properties - Adam Brown.png"/> 

<img width="1000" height="800" alt="User's new dynamic group assignment" src="images/Mover - New DG - Adam Brown.png"/> 

<img width="1000" height="800" alt="User Sign-In Log Confirmation" src="images/Mover - App Sign-in Log - Adam Brown.png"/> 

<img width="1000" height="800" alt="User Sign-In Audit Logs Confirmation" src="images/Mover - Sign-in Activity - Adam Brown.png"/> 

## 📘 Leaver of J-M-L:

User `Michelle Smith` is leaving the organization.
- Users profile was disabled via user properties
- User was unable to sign-in
- Sign-in logs indicate an unsuccessfull log-in

<img width="1000" height="800" alt="Account disabled in Entra ID" src="images/Leaver - Account Disabled - Michelle Smith.png"/> 

<img width="1000" height="800" alt="Disabled user sign-in attempt" src="images/Leaver - Signon Attempt - Michelle Smith.png"/> 

<img width="1000" height="800" alt="Error message when user attempts to sign in" src="images/Leaver - Account Disabled Confirmation - Michelle Smith.png"/> 

<img width="1000" height="800" alt="Sign-in logs confirming user was unable to log-in" src="images/Leaver - SigninLog Showing Failure - Michelle Smith.png"/> 



