---
title: Responding to a Compromised Email Account
f1.keywords: 
  - NOCSH
  - Hijacked account
  - Hacked account
  - Compromised account
ms.author: chrisda
author: chrisda
manager: deniseb
audience: ITPro
ms.topic: how-to
ms.collection: 
  - o365_security_incident_response
  - m365-security
  - m365solution-smb
  - highpri
  - tier1
ms.custom: 
  - TopSMBIssues
  - seo-marvel-apr2020
ms.localizationpriority: high
search.appverid: 
  - MET150
description: Learn how to recognize and respond to a compromised email account using tools available in Microsoft 365.
ms.service: defender-office-365
ms.date: 06/10/2024
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Exchange Online Protection</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# Responding to a compromised email account

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

Credentials control access to Microsoft 365 mailboxes, data, and other services. When someone steals those credentials, the associated account is considered to be compromised.

After an attacker steals the credentials and gains access to the account, they can access the associated Microsoft 365 mailbox, SharePoint folders, or files in the user's OneDrive. Attackers often use the compromised mailbox to send email as the original user to recipients inside and outside of the organization. Attackers using email to send data to external recipients is known as _data exfiltration_.

This article explains the symptoms of account compromise and how to regain control of the compromised account.

## Symptoms of a compromised Microsoft email account

Users might notice and report unusual activity in their Microsoft 365 mailboxes. For example:

- Suspicious activity, such as missing or deleted email.
- Users receiving email from the compromised account without the corresponding email in the sender's **Sent Items** folder.
- Suspicious Inbox rules. These rules might automatically forward email to unknown addresses or move messages to the **Notes**, **Junk Email**, or **RSS Subscriptions** folders.
- The user's display name is changed in the Global Address List.
- The user's mailbox is blocked from sending email.
- The **Sent Items** or **Deleted Items** folders in Microsoft Outlook or Outlook on the web (formerly known as Outlook Web App) contain typical messages for compromised accounts (for example, "I'm stuck in London, send money.").
- Unusual profile changes. For example, name, telephone number, or postal code updates.
- Multiple and frequent password changes.
- Recently added external email forwarding.
- Unusual email message signatures. For example, a fake banking signature or a prescription drug signature.

You need to immediately investigate if a user reports these or other unusual symptoms. The Microsoft Defender portal and the Azure portal offer the following tools to help you investigate suspicious activity on a user account:

- **Unified audit logs in the Microsoft Defender portal**: Filter the logs for activity using a date range that starts immediately before the suspicious activity occurred to today. Don't filter on specific activities during the search. For more information, see [Search the audit log](audit-log-search-defender-portal.md).

- **Microsoft Entra sign-in logs and other risk reports in the Microsoft Entra admin center**: Examine the values in these columns:
  - Review IP address
  - sign-in locations
  - sign-in times
  - sign-in success or failure

> [!IMPORTANT]
> The following button lets you test and identify suspicious account activity. You can use this information to recover a compromised account.
>
<div class="nextstepaction">
<p><a href="https://aka.ms/diagca" data-linktype="external">Run Tests: Compromised Accounts</a></p>
</div>

## Secure and restore email function to a compromised Microsoft 365 account and mailbox

<!--- [!VIDEO https://videoplayercdn.osi.office.net/hub/?csid=ux-cms-en-us-msoffice&uuid=RE2jvOb&AutoPlayVideo=false] --->

Even after the user regains access to their account, the attacker might leave back-door entries that can regain control of the account.

Do **all** of the following steps to regain control of the account. Go through the steps as soon as you suspect a problem and as quickly as possible to make sure that the attacker doesn't regain control of the account. These steps also help you remove any back-door entries that the attacker added to the account. After you do these steps, we recommend that you run a virus scan to make sure that the client computer isn't compromised.

### Step 1: Reset the user's password

Follow the procedures in [Reset a business password for someone](/microsoft-365/admin/add-users/reset-passwords#reset-my-admin-password).

> [!IMPORTANT]
>
> - Don't send the new password to the user through email, because the attacker still has access to the mailbox at this point.
>
> - Be sure to use a strong password: upper and lowercase letters, at least one number, and at least one special character.
>
> - Even if the password history requirement allows it, don't reuse any of the last five passwords. Use a unique password that the attacker can't guess.
>
> - If the user's identity is federated with Microsoft 365, you must change the account password in the on-premises environment, and then notify the administrator of the compromise.
>
> - Be sure to update app passwords. App passwords aren't automatically revoked when you reset the password. The user should delete existing app passwords and create new ones. For instructions, see [Manage app passwords for two-step verification](https://support.microsoft.com/account-billing/d6dc8c6d-4bf7-4851-ad95-6d07799387e9).
>
> - We highly recommended that you enable multi-factor authentication (MFA) for the account. MFA is a good way to help prevent account compromise, and is very important for accounts with administrative privileges. For instructions, see [Set up multi-factor authentication](/microsoft-365/admin/security-and-compliance/set-up-multi-factor-authentication).

### Step 2: Remove suspicious email forwarding addresses

1. In the Microsoft 365 admin center at <https://admin.microsoft.com>, go to **Users** \> **Active users**. Or, to go directly to the **Active users** page, use <https://admin.microsoft.com/Adminportal/Home#/users>.

2. On the **Active users** page, find the user account, and select it by clicking anywhere in the row other than the check box next to the name.

3. In the details flyout that opens, select the **Mail** tab.

4. On the **Mail** tab, the value **Applied** in the **Email forwarding** section indicates that mail forwarding is configured on the account. To remove it, do the following steps:
   - Select **Manage email forwarding**.
   - In the **Manage email forwarding** flyout that opens, clear the **Forward all email sent to this mailbox** check box, and then select **Save changes**.

### Step 3: Disable suspicious Inbox rules

1. Sign in to the user's mailbox using Outlook on the web.

2. Select **Settings** (gear icon), enter 'rules' in the :::image type="icon" source="media/m365-cc-sc-search-icon.png" border="false"::: **Search settings** box, and then select **Inbox rules** in the results.

3. On the **Rules** flyout that opens, review the existing rules, and turn off or delete any suspicious rules.

### Step 4: Unblock the user from sending mail

If the account was used to send spam or a high volume of email, it's likely that the mailbox is blocked from sending mail.

To unblock a mailbox from sending email, follow the procedures in [Remove blocked users from the Restricted entities page](outbound-spam-restore-restricted-users.md).

### Step 5 Optional: Block the user account from signing-in

> [!IMPORTANT]
> You can block the account from signing-in until you believe it's safe to re-enable access.

1. Do the following steps in the Microsoft 365 admin center at <https://admin.microsoft.com>:
   1. Go to **Users** \> **Active users**. Or, to go directly to the **Active users** page, use <https://admin.microsoft.com/Adminportal/Home#/users>.
   2. On the **Active users** page, find and select the user account from the list by doing one of the following steps:
      - Select the user by clicking anywhere in the row other than the check box next to the name. In the details flyout that opens, select :::image type="icon" source="media/m365-cc-sc-no-icon.png" border="false"::: **Block sign-in** at the top of the flyout.
      - Select the user by selecting the check box next to the name. Select :::image type="icon" source="media/m365-cc-sc-more-actions-icon.png" border="false"::: **More actions** \> :::image type="icon" source="media/m365-cc-sc-no-icon.png" border="false"::: **Edit sign-in status**.
   3. In the **Block sign-in** flyout that opens, read the information, select **Block this user from signing in**, select **Save changes**, and then select :::image type="icon" source="media/m365-cc-sc-close-icon.png" border="false"::: **Close** at the top of the flyout.

2. Do the following steps in the Exchange admin center (EAC) at <https://admin.exchange.microsoft.com>:
   1. Go to **Recipients** \> **Mailboxes**. Or, to go directly to the **Mailboxes** page, use <https://admin.exchange.microsoft.com/#/mailboxes>.
   2. On the **Manage mailboxes** page, find and select the user from the list by clicking anywhere in the row other than the round check box that appears next to the name.
   3. In the details flyout that opens, do the following steps:
      1. Verify the **General** tab is selected, and then select **Manage email apps settings** in the **Email apps & mobile devices** section.
      2. In the **Manage settings for email apps** flyout that opens, disable all of the available settings by changing the toggles to :::image type="icon" source="media/scc-toggle-off.png" border="false"::: **Disabled**:
         - **Outlook desktop (MAPI)**
         - **Exchange Web Services**
         - **Mobile (Exchange ActiveSync)**
         - **IMAP**
         - **POP3**
         - **Outlook on the web**

      When you're finished in the **Manage settings for email apps** flyout, select **Save**, and then select :::image type="icon" source="media/m365-cc-sc-close-icon.png" border="false"::: **Close** at the top of the flyout.

### Step 6 Optional: Remove the suspected compromised account from all administrative roles

> [!NOTE]
> You can restore the user's membership in administrative roles after the account has been secured.

1. In the Microsoft 365 admin center at <https://admin.microsoft.com>, do the following steps:
   1. Go to **Users** \> **Active users**. Or, to go directly to the **Active users** page, use <https://admin.microsoft.com/Adminportal/Home#/users>.
   2. On the **Active users** page, find and select the user account from the list by doing one of the following steps:
      - Select the user by clicking anywhere in the row other than the check box next to the name. In the details flyout that opens, verify the **Account** tab is selected, and then select **Manage roles** in the **Roles** section.
      - Select the user by selecting the check box next to the name. Select :::image type="icon" source="media/m365-cc-sc-more-actions-icon.png" border="false"::: **More actions** \> :::image type="icon" source="media/m365-cc-sc-manage-roles-icon.png" border="false"::: **Manage roles**.
   3. In the **Manage admin roles** flyout that opens, do the following steps:
      - Record any information that you want to restore later.
      - Remove administrative role membership by selecting **User (no admin center access)**.

      When you're finished in the **Manage admin roles** flyout, select **Save changes**.

2. In the Microsoft Defender portal at <https://security.microsoft.com>, do the following steps:
   1. Go to **Permissions** \> **Email & collaboration roles** \> **Roles**. Or, to go directly to the **Permissions** page, use <https://security.microsoft.com/emailandcollabpermissions>.
   2. On the **Permissions** page, select a role group from the list by selecting the check box next to the name (for example, **Organization Management**), and then selecting :::image type="icon" source="media/m365-cc-sc-edit-icon.png" border="false"::: **Edit** action that appears.
   3. In the **Edit members of the role group** page that opens, review the list of members. If the role group contains the user account, remove the user by selecting the check box next to the name, and then selecting :::image type="icon" source="media/m365-cc-sc-delete-icon.png" border="false"::: **Remove members**.

      When you're finished on the **Edit members of the role group** page, select **Next**

   4. On the **Review the role group and finish** page, review the information, and then select **Save**.
   5. Repeat the previous steps for each role group in the list.

3. In the Exchange admin center at <https://admin.exchange.microsoft.com/>, do the following steps:
   1. Go to **Roles** \> **Admin roles**. Or to go directly to the **Admin roles** page, use <https://admin.exchange.microsoft.com/#/adminRoles>.
   2. On the **Admin roles** page, select a role group from the list by clicking anywhere in the row other than the round check box that appears next to the name.
   3. In the details flyout that opens, select the **Assigned** tab, and then look for the user account. If the role group contains the user account, do the following steps:
      1. Select the user account by selecting the round check box that appears next to the name.
      2. Select the :::image type="icon" source="media/m365-cc-sc-delete-icon.png" border="false"::: **Delete** action that appears, select **Yes, remove** in the warning dialog, and then select :::image type="icon" source="media/m365-cc-sc-close-icon.png" border="false"::: **Close** at the top of the flyout.

   4. Repeat the previous steps for each role group in the list.

### Step 7 Optional: Additional precautionary steps

1. Verify the contents of the **Sent items** folder of the account in Outlook or Outlook on the web.

   You might need to inform the user's contacts that the account was compromised. For example, the attacker might have sent messages asking contacts for money, or the attacker might have sent a virus to hijack their computers.

2. Other services that use this account as an alternative email address might also be compromised. After you do the steps in this article for the account in this Microsoft 365 organization, do the corresponding steps in the other services.

3. Verify the contact information (for example, telephone numbers and addresses) of the account.

## See also

- [Detect and Remediate Outlook Rules and Custom Forms Injections Attacks in Microsoft 365](detect-and-remediate-outlook-rules-forms-attack.md)
- [Detect and Remediate Illicit Consent Grants](detect-and-remediate-illicit-consent-grants.md)
- [Internet Crime Complaint Center](https://www.ic3.gov/Home/Ransomware)
- [Securities and Exchange Commission - "Phishing" Fraud](https://www.sec.gov/investor/pubs/phishing.htm)
- [Report messages as phishing](https://support.microsoft.com/office/9ba3ea70-1169-4993-801b-ec2bb8fc071d) to Microsoft and/or admins (depending on how [User reported settings](submissions-user-reported-messages-custom-mailbox.md) are configured in the organization).
