# 🔎 Attribute Based Access Controls (ABAC) for Joiner - Mover - Leaver Identity Lifecycle Management Project

**Platform:** Microsoft Entra ID  
**Focus:** Identity Lifecycle Management, Automation, Dynamic Groups, Enterprise App Access, Conditional Access**


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
- Access to `CA-Policy-Test-App` confirmed via `Sign-In` and `Audit` logs
- User was prompted to update their password upon signing-in for the first time
- User was prompted to utilize MS Authenticator and was able to successfully enroll.
- Sign-In logs confirmed the `Conditional Access Policy` was triggered and user successfully met the requirement.

<img width="1000" height="800" alt="User Sign-In password prompt" src="images/User Sign-In - Jason  - Password Prompt.png"/> 
