# Microsoft Entra ID: Users and Groups

This lab covers the fundamentals of identity management in Microsoft Entra ID (formerly Azure AD): creating user accounts, inviting external (guest) users, and organizing both into groups for access control.

## Overview

Users and groups are the basic building blocks of any identity solution. In this lab, I provisioned internal and guest user accounts in Microsoft Entra ID and organized them into a security group, simulating how an organization would onboard engineers into a new pre-production lab environment.

## Lab Scenario

An organization is standing up a new lab environment for pre-production testing of apps and services. A small number of engineers are being hired to manage that environment, including its virtual machines. To let those engineers authenticate through Microsoft Entra ID, I was tasked with provisioning users and groups — with the goal of keeping group membership easy to manage as the team grows.

## Environment

- Azure subscription
- Microsoft Entra ID (Azure AD)
- Region: East US

## Architecture

![Lab architecture diagram](https://github.com/user-attachments/assets/7e8a9549-f56a-4e67-ae04-02daa931e724)

## Skills Practiced

- Creating and configuring Microsoft Entra ID user accounts
- Inviting and configuring external (guest) users
- Creating security groups and managing membership
- Understanding tenants, static vs. dynamic group membership, and Entra ID licensing implications

---

## Task 1: Create and Configure User Accounts

User accounts store identity data such as name, department, location, and contact information. In this task, I created a native Entra ID user and invited an external guest user, then configured both with matching job/department metadata.

### Step 1: Open Microsoft Entra ID

In the Azure portal, search for **Microsoft Entra ID** and select it. Entra ID is Azure's cloud-based identity and access management service.

### Step 2: Review tenant information

From the **Overview** blade, select the **Manage tenants** tab.

> A tenant is a dedicated instance of Microsoft Entra ID that holds an organization's accounts and groups. Depending on your setup, you can create additional tenants and switch between them.

![Manage tenants view](https://github.com/user-attachments/assets/3977c45f-bbf4-4b1a-b92d-7f35fdfdcb51)

### Step 3: Create a new user

In the **Manage** blade, select **Users**, then from the **New user** dropdown select **Create new user**.

> This opens a new browser tab — select **New user** again once it loads.

![Create new user menu](https://github.com/user-attachments/assets/425a22f2-a63a-4caf-abf4-ece29968644a)

### Step 4: Set the user's basic info

Name the user anything you'd like.

![New user basic info](https://github.com/user-attachments/assets/41aeb488-54a7-478b-a7cb-f335e0075e81)

### Step 5: Fill in the Properties tab

| Setting | Value |
|---|---|
| Job title | IT Lab Administrator |
| Department | IT |
| Usage location | United States |

### Step 6: Review and create

Select **Review + create**, confirm the details, and create the user. Your summary should resemble the screenshot below (your specific values will differ based on what you entered).

![Review and create user](https://github.com/user-attachments/assets/e013f04f-4c06-45ee-80c3-56f5987e42ee)

### Step 7: Confirm the user was created

Refresh the **Users** page and confirm the new account appears in the list.

![New user appears in users list](https://github.com/user-attachments/assets/9e947d93-fb32-4f3d-9f63-80a925ac3dc0)

### Step 8: Invite an external user

From the **New user** dropdown, select **Invite an external user**.

**Settings:**

| Setting | Value |
|---|---|
| Email | Your email address |
| Display name | Your name |
| Send invite message | Checked |
| Message | Hey, you're invited to check out the IT lab environment I'm setting up in Azure. Welcome aboard! |

### Step 9: Configure the guest user's properties

Move to the **Properties** tab and fill in the same fields used for the internal user:

| Setting | Value |
|---|---|
| Job title | IT Lab Administrator |
| Department | IT |
| Usage location | United States |

`[ADD SCREENSHOT HERE — guest invite Properties tab]`

### Step 10: Send the invite

Select **Review + invite**, then **Invite**.

### Step 11: Confirm the guest user was created

Refresh the page and confirm the invited (guest) user now appears in the list. You should also receive the invitation email shortly.

`[ADD SCREENSHOT HERE — guest user listed]`

> **Reflection:** Creating accounts one at a time doesn't scale. Most organizations provision users in bulk — through CSV import, PowerShell/Graph API scripts, or automated HR-driven provisioning (e.g. via Entra ID Connect or an HR system integration).

---

## Task 2: Create Groups and Add Members

Groups can contain users or devices, and membership can be assigned in two ways:

- **Static** — an admin manually adds and removes members
- **Dynamic** — membership updates automatically based on a rule, such as job title (requires Entra ID Premium P1 or P2)

### Step 1: Open Groups

In the Azure portal, search for and select **Microsoft Entra ID**, then in the **Manage** blade select **Groups**.

### Step 2: Review group settings

Take a moment to look through the group settings in the left pane:

- **Expiration** — sets a group lifetime in days; after that period, the owner must renew it
- **Naming policy** — lets you block certain words and enforce a prefix/suffix on group names

`[ADD SCREENSHOT HERE — group settings pane]`

### Step 3: Create a new group

From **All groups**, select **+ New group**.

| Setting | Value |
|---|---|
| Group type | Security |
| Group name | IT Lab Administrators |
| Group description | Administrators that manage the IT lab |
| Membership type | Assigned |

> Dynamic membership requires an Entra ID Premium P1 or P2 license. If your tenant has one, additional membership type options will appear in the dropdown.

![Create assigned group](https://github.com/user-attachments/assets/e013f04f-4c06-45ee-80c3-56f5987e42ee)

### Step 4: Add an owner

Select **No owners selected**, then search for and select yourself as the owner.

> A group can have more than one owner.

`[ADD SCREENSHOT HERE — add owners pane]`

### Step 5: Add members

Select **No members selected**. In the **Add members** pane, search for and select the user account and guest user created in Task 1, then add both to the group.

`[ADD SCREENSHOT HERE — add members pane]`

### Step 6: Create the group

Select **Create** to deploy the group.

### Step 7: Confirm the group was created

Refresh the page and confirm the new group appears in the group list.

`[ADD SCREENSHOT HERE — group list showing new group]`

### Step 8: Review group membership

Open the new group and review its **Members** and **Owners** tabs to confirm everything was added correctly.

`[ADD SCREENSHOT HERE — members/owners tab]`

> **Reflection:** At scale, managing groups individually becomes unsustainable. A real plan would define naming conventions, ownership rules, and a process (manual or automated) for adding/removing members as staff join or change roles.

---

## Key Takeaways

- A **tenant** represents an organization's dedicated instance of Microsoft cloud services, covering both internal and external (guest) users.
- Microsoft Entra ID supports both **user** and **guest** accounts, each scoped to the access appropriate for their role.
- **Groups** combine related users or devices, and come in two types: **Security** and **Microsoft 365**.
- Group membership can be assigned **statically** (manual) or **dynamically** (rule-based, requires Premium licensing).













