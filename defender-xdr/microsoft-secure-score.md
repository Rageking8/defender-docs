---
title: Microsoft Secure Score
description: Describes Microsoft Secure Score in the Microsoft Defender portal, how to improve your security posture, and what security admins can expect.
ms.service: defender-xdr
ms.localizationpriority: medium
f1.keywords:
  - NOCSH
ms.author: deniseb
author: denisebmsft
manager: dansimp
audience: ITPro
ms.collection:
- m365-security
- Adm_TOC
- tier2
ms.topic: conceptual
search.appverid:
- MOE150
- MET150
ms.date: 09/29/2024
---

# Microsoft Secure Score

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

Microsoft Secure Score is a measurement of an organization's security posture, with a higher number indicating more recommended actions taken. It can be found at [Microsoft Secure Score](https://security.microsoft.com/securescore) in the Microsoft Defender portal.

Following the Secure Score recommendations can protect your organization from threats. From a centralized dashboard in the Microsoft Defender portal, organizations can monitor and work on the security of their Microsoft 365 identities, apps, and devices.

Secure Score helps organizations:

- Report on the current state of the organization's security posture.
- Improve their security posture by providing discoverability, visibility, guidance, and control.
- Compare with benchmarks and establish key performance indicators (KPIs).

Watch this video for a quick overview of Secure score.
> [!VIDEO https://learn-video.azurefd.net/vod/player?id=7a45971a-f075-48b9-b8f1-1f7f20152a73]

Organizations gain access to robust visualizations of metrics and trends, integration with other Microsoft products, score comparison with similar organizations, and much more. The score can also reflect when non-Microsoft solutions addressed recommended actions.

:::image type="content" source="/defender/media/secure-score/secure-score-home-page.png" alt-text="Screenshot that shows the Microsoft Secure Score homepage in the Microsoft Defender portal" lightbox="/defender/media/secure-score/secure-score-home-page.png":::

## How it works

You get points for the following actions:

- Configuring recommended security features
- Doing security-related tasks
- Addressing the recommended action with a non-Microsoft application or software, or an alternate mitigation

Some recommended actions only give points when fully completed. Some actions result in partial points if tasks are completed for some devices or users. If you can't or don't want to enact one of the recommended actions, you can choose to accept the risk or remaining risk.

If you have a license for one of the supported Microsoft products, then you see recommendations for those products. We show you the full set of possible recommendations for a product, regardless of license edition, subscription, or plan. This way, you can understand security best practices and improve your score. Your absolute security posture, represented by Secure Score, stays the same no matter what licenses your organization owns for a specific product. Keep in mind that security should be balanced with usability, and not every recommendation can work for your environment.

Your score is updated in real time to reflect the information presented in the visualizations and recommended action pages. Secure Score also syncs daily to receive system data about your achieved points for each action.

> [!NOTE]
> For Microsoft Teams and Microsoft Entra related recommendations, the recommendation state will get updated when changes occur in the configuration state. In addition, the recommendation state is refreshed once a month or once a week, respectively.

### Key scenarios

- [Check your current score](microsoft-secure-score-improvement-actions.md#check-your-current-score)
- [Compare your score to organizations like yours](microsoft-secure-score-history-metrics-trends.md#compare-your-score-to-organizations-like-yours)
- [View recommended actions and decide an action plan](microsoft-secure-score-improvement-actions.md#take-action-to-improve-your-score)
- [Initiate work flows to investigate or implement](microsoft-secure-score-improvement-actions.md#view-recommended-action-details)

### How recommended actions are scored

Each recommended action is worth 10 points or less, and most are scored in a binary fashion. If you implement the recommended action, like create a new policy or turn on a specific setting, you get 100% of the points. For other recommended actions, points are given as a percentage of the total configuration.

For example, a recommended action states you get 10 points by protecting all your users with multifactor authentication. You only have 50 of 100 total users protected, so you'd get a partial score of five points (50 protected / 100 total * 10 max pts = 5 pts).

### Products included in Secure Score

Currently there are recommendations for the following products:

- App governance
- Microsoft Entra ID
- Citrix ShareFile
- Microsoft Defender for Endpoint
- Microsoft Defender for Identity
- Microsoft Defender for Office
- Docusign
- Exchange Online
- GitHub
- Microsoft Defender for Cloud Apps
- Microsoft Purview Information Protection
- Microsoft Teams
- Okta
- Salesforce
- ServiceNow
- SharePoint Online
- Zoom

Recommendations for other security products are coming soon. The recommendations don't cover all the attack surfaces associated with each product, but they're a good baseline. You can also mark the recommended actions as covered by a non-Microsoft solution or alternate mitigation.

### Security defaults

Microsoft Secure Score includes updated recommended actions to support [security defaults in Microsoft Entra ID](/azure/active-directory/fundamentals/concept-fundamentals-security-defaults to make it easier to help protect your organization with preconfigured security settings for common attacks.

If you turn on security defaults, you are awarded full points for the following recommended actions:

- Ensure all users can complete multifactor authentication for secure access (nine points)
- Require MFA for administrative roles (10 points)
- Enable policy to block legacy authentication (seven points)

> [!IMPORTANT]
> Security defaults include security features that provide similar security to the sign-in risk policy and user risk policy recommended actions. Instead of setting up these policies on top of the security defaults, we recommend updating their statuses to `Resolved through alternative mitigation`.

## Secure Score permissions

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

<a name='manage-permissions-with-microsoft-365-defender-unified-role-based-access-controlrbac'></a>

### Manage permissions with Microsoft Defender XDR Unified role-based access control (RBAC)

With [Microsoft Defender XDR Unified role-based access control(RBAC)](manage-rbac.md), you can create custom roles with specific permissions for Secure Score. These permissions are located under the **Security posture** category in Defender XDR Unified RBAC permissions model and are named **Exposure Management (read)** for read-only access and **Exposure Management (manage)** for users who will have access to manage Secure Score recommendations.

In order for users to access Secure Score data, a custom role in Defender XDR Unified RBAC shall be assigned with the **Microsoft Security Exposure Management** data source.

To start using Microsoft Defender XDR Unified RBAC to manage your Secure Score permissions, see [Microsoft Defender XDR Unified role-based access control (RBAC)](manage-rbac.md).

> [!NOTE]
> Defender XDR Unified RBAC is automatically active for Secure Score access. Once a custom role with one of the permissions is created, it has an immediate impact on assigned users. There is no need to activate it.
> 
> Currently, the model is only supported in the Microsoft Defender portal. If you want to use GraphAPI (for example, for internal dashboards or Defender for Identity Secure Score) you should continue to use Microsoft Entra roles. Support GraphAPI is planned at a later date.

<a name='azure-active-directory-global-roles-permissions'></a>

### Microsoft Entra global roles permissions

Microsoft Entra global roles (for example, Global Administrator) can still be used to access Secure Score. Users who have the supported Microsoft Entra global roles, but aren't assigned to a custom role in Microsoft Defender XDR Unified RBAC continue to have access to view (and manage where permitted) Secure Score data as outlined:

The following roles have read and write access and can make changes, directly interact with Secure Score, and can assign read-only access to other users:

- Global Administrator
- Security Administrator
- Exchange Administrator
- SharePoint Administrator

The following roles have read-only access and aren't able to edit status or notes for a recommended action, edit score zones, or edit custom comparisons:

- Helpdesk Administrator
- User Administrator
- Service Support Administrator
- Security Reader
- Security Operator
- Global Reader

> [!NOTE]
> If you want to follow the principle of least privilege access (where you only give users and groups the permissions, they need to do their job), Microsoft recommends that you remove any existing elevated Microsoft Entra global roles for users and/or security groups assigned a custom role with Secure Score permissions. This will ensure that the custom Microsoft Defender XDR Unified RBAC roles will take effect.

## Risk awareness

Microsoft Secure Score is a numerical summary of your security posture based on system configurations, user behavior, and other security-related measurements. It isn't an absolute measurement of how likely your system or data could be breached. Rather, it represents the extent to which you are using security controls in your Microsoft environment that can help offset the risk of being breached. No online service is immune from security breaches, and secure score shouldn't be interpreted as a guarantee against security breach in any manner.

## We want to hear from you

If you have any issues, let us know by posting in the [Security, Privacy & Compliance](https://techcommunity.microsoft.com/t5/Security-Privacy-Compliance/bd-p/security_privacy) community.

## Related resources

- [Assess your security posture](microsoft-secure-score-improvement-actions.md)
- [Track your Microsoft Secure Score history and meet goals](microsoft-secure-score-history-metrics-trends.md)
- [What's coming](whats-new.md)
- [What's new](microsoft-secure-score-whats-new.md)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
