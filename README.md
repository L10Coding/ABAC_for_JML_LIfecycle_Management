# 🔎 Attribute-Based Access Controls (ABAC) for Joiner-Mover-Leaver (JML) Identity Lifecycle Management

**Platform:** Microsoft Entra ID  
**Focus:** Identity Lifecycle Management (ILM), Automation, Dynamic Groups, Enterprise App Access, Conditional Access (CA)**

---

# 👔 Executive Summary
In modern enterprise environments, managing user access manually creates operational bottlenecks and severe security vulnerabilities. This project demonstrates a fully automated Joiner-Mover-Leaver (JML) identity lifecycle built in Microsoft Entra ID using Attribute-Based Access Control (ABAC).

By leveraging core user attributes (such as Department and Job Title) as a dynamic source of truth, this architecture eliminates the need for manual administrative tickets. It automatically provisions resources for new hires, realigns security boundaries during internal role changes, and enforces instant access revocation during offboarding. The entire lifecycle is wrapped in context-aware Conditional Access (CA) policies to ensure a zero-trust security posture.

---

# 🚀 Key Takeaways & Business Impact
- **Zero-Touch Provisioning:** Reduced administrative overhead by automating group memberships and application assignments.
- **Elimination of Access Creep:** Solved a major compliance issue by ensuring users automatically lose old privileges when changing roles.
- **Instant Risk Mitigation:** Secured corporate data by verifying that disabled "Leaver" accounts are immediately blocked from all enterprise resources.
- **Audit-Ready Infrastructure:** Validated every identity lifecycle transition using Entra ID Sign-In and Audit logs to prove compliance.

---

# 📘 Project Overview

This project showcases the practical implementation of ABAC to control identity lifecycles. The system uses account attributes to automatically handle:
- *Group Membership*
- *Application Access*
- *Conditional Access Policies*
- *Account Revocation*

I used Entra ID Group membership and Sign-In/Audit Logs to verify that every step worked as intended.

---

# 👥 Phase 1: The "Joiner" Process (User Onboarding)
The **Joiner** phase focuses on onboarding new hires safely and quickly. When a user account is created with specific corporate attributes, Entra ID places them into the correct security boundaries automatically.


## 1.  Adding Users to the environment

I created three users with different department and title attributes: Adam Brown, Jason Jones and Michelle Smith

| User | Department | Job Title |
|-----|------------|-----------|
| Adam Brown | Marketing | Content Strategist
| Jason Jones | Sales | Sales Analyst |
| Michelle Smith | Human Resources | Human Resources Analyst |

##   Configuration proof:
First User:
<img width="1000" height="800" alt="User Adam Brown confirmation" src="images/Adam Brown - Properties.jpg"/> 

Second User:
<img width="1000" height="800" alt="User Jason Jones confirmation" src="images/Jason Jones - Properties.jpg"/> 

Third User:
<img width="1000" height="800" alt="User Michelle Smith confirmation" src="images/Michelle Smith - Properties.jpg"/> 

---

## 2. Creating Dynamic Security Groups

I built **Dynamic Groups** that will access user atributes to manage membership automatically.

**Verification of Automated Membership:**
The system scanned the user attributes and automatically sorted the users into their proper groups.

<img width="1000" height="800" alt="Dynamic Group Creation - Marketing" src="images/Dynamic Group Creation - Marketing.jpg"/> 


**Confirmation of Dynamic Groups created for each department:**

<img width="1000" height="800" alt="Dynamic Group List" src="images/Dynamic Groups List.png"/> 


**Policy ran correctly, and now shows the users as members of their respective Dynamic Group:**

<img width="1000" height="800" alt="Dynamic Group Membership - HR" src="images/Dynamic Group Membership - HR.png"/> 

<img width="1000" height="800" alt="Dynamic Group Membership - Sales" src="images/Dynamic Group Membership - Sales.png"/> 

<img width="1000" height="800" alt="Dynamic Group Membership - Marketing" src="images/Dynamic Group Membership - Marketing.jpg"/> 

---

## 3. Setting Up the Enterprise App `(CA-Policy-Test-App)`:

Deployed a test app named `CA-Policy-Test-App` and configured it for secure access:
- Enabled the Assignment Required setting, so that only designated users can access.
- Assigned the Dynamic Groups to the app.
- Configured Single Sign-On (SSO) and SAML, so that users can sign in securely with their Entra ID credentials.

<img width="1000" height="800" alt="Policy-Test App Configuration" src="images/CA-CA Policy Test App - Properties.png "/> 

<img width="1000" height="800" alt="Policy-Test App Assigned Groups" src="images/CA-CA Policy Test App - Applicable Groups.png "/> 

---

## 4. Establishing Conditional Access Policies according to Dynamic Group/Department
To add an additional layer of protection, I created specific security rules tailored to each group's attributes:

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


## 5. Testing the **Joiner** Experience:

Logged in as user `Jason Jones` to verify the onboarding workflow:
- User was prompted to update their password upon signing-in for the first time
- User was prompted to utilize MS Authenticator and was able to successfully enroll.
- Logs confirmed the Sales Session Control policy triggered correctly, and the Marketing MFA policy did not affect him, proving the policy targets users accurately.

<img width="1000" height="800" alt="User Sign-In password prompt" src="images/User Sign-In - Jason  - Password Prompt.png"/> 

<img width="1000" height="800" alt="User Sign-In Authenticator Added" src="images/User Sign-In - Authenticator Added.png"/> 

<img width="1000" height="800" alt="User Sign-In Audit Logs Confirmation" src="images/App Audit Logs - Jason Jones.png"/> 

<img width="1000" height="800" alt="User Sign-In Audit Logs Confirmation" src="images/App Sign-In Activity Details - Jason Jones.png"/> 


## 🔄 Phase 2: The "Mover" Process (Role Transitions):

The **Mover** phase handles internal job changes. ABAC solves access creep—the dangerous problem where employees keep old permissions when they switch roles.

Role transition scenario:
- Changed `Adam Brown's` attributes to move him from Marketing to Sales.
- The Automation works: Changing his profile attributes triggered recalculation of his groups/memberships.
- Old Access Dropped: He was removed from **Marketing** and lost access to Marketing resources.
- New Access Granted: He was added to **Sales** and gained access to Sales tools.
- Security Updated: His access to `CA-Policy-Test-App` remained, and the **Sales Session Control** policy applied to him automatically. 

<img width="1000" height="800" alt="Updating user properties" src="Mover - Updating Properties - Adam Brown.png"/> 

<img width="1000" height="800" alt="User's new dynamic group assignment" src="images/Mover - New DG - Adam Brown.png"/> 

<img width="1000" height="800" alt="User Sign-In Log Confirmation" src="images/Mover - App Sign-in Log - Adam Brown.png"/> 

<img width="1000" height="800" alt="User Sign-In Audit Logs Confirmation" src="images/Mover - Sign-in Activity - Adam Brown.png"/> 

## 🚪 Phase 3: The "Leaver" Process (Offboarding & De-provisioning):
The Leaver phase secures the business when a worker departs. Disabling access quickly stops former workers from accessing company files from the outside.

Offboarding Scenario:

`Michelle Smith` left the organization. I disabled her profile to simulate the leaver workflow.

- Instant Lockdown: The account status changed to disabled
- Sign-In Blocked: Michelle was stopped at the front door during her next sign-in attemptl
- Audit Proof: The Entra ID Sign-In logs caught the failed attempt and flagged it as an unsuccessful login due to a disabled account.

<img width="1000" height="800" alt="Account disabled in Entra ID" src="images/Leaver - Account Disabled - Michelle Smith.png"/> 

<img width="1000" height="800" alt="Disabled user sign-in attempt" src="images/Leaver - Signon Attempt - Michelle Smith.png"/> 

<img width="1000" height="800" alt="Error message when user attempts to sign in" src="images/Leaver - Account Disabled Confirmation - Michelle Smith.png"/> 

<img width="1000" height="800" alt="Sign-in logs confirming user was unable to log-in" src="images/Leaver - SigninLog Showing Failure - Michelle Smith.png"/> 



