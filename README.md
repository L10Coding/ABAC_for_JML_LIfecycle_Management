# 🔎 Attribute Based Access Controls (ABAC) for Joiner - Mover - Leaver Identity Lifecycle Management Project

**Platform:** Microsoft Entra ID  
**Focus:** Identity Lifecycle Management, Automation, Dynamic Groups, Enterprise App Access, Conditional Access**

💻

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

##  📝 Creatinging Dynamic Security Groups

Created Dynamic Groups that will assign membership according to the user's attributes (Job Title):

<img width="1000" height="800" alt="Dynamic Group Creation - Marketing" src="images/Dynamic Group Creation - Marketing.jpg"/> 

**Confirmation of Dynamic Groups created for each department:**

<img width="1000" height="800" alt="Dynamic Group List" src="images/Dynamic Groups List.png"/> 

**Policy ran correctly, and now shows the Marketing user(s) as a member of the Dynamic Group "DG-Marketing-Users":**

<img width="1000" height="800" alt="Dynamic Group Membership - HR" src="images/Dynamic Group Membership - HR.jpg"/> 

<img width="1000" height="800" alt="Dynamic Group Membership - Sales" src="images/Dynamic Group Membership - Sales.jpg"/> 

<img width="1000" height="800" alt="Dynamic Group Membership - Marketing" src="images/Dynamic Group Membership - Marketing.jpg"/> 

