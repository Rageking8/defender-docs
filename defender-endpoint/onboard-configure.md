---
title: Onboard devices and configure Microsoft Defender for Endpoint capabilities
description: Onboard Windows 10 and Windows 11 devices, servers, non-Windows devices and learn how to run a detection test.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier2
ms.topic: conceptual
ms.subservice: onboard
search.appverid: met150
ms.date: 09/30/2024
---

# Configure Microsoft Defender for Endpoint capabilities

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

[!include[Prerelease information](../includes/prerelease.md)]

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

In this step, you're ready to configure Microsoft Defender for Endpoint capabilities.

## Configure capabilities

In many cases, organizations have existing endpoint security products in place. The bare minimum being an antivirus solution, but in some cases, an organization might have existing endpoint detection and response solution.

It's common that Defender for Endpoint needs to exist along side these existing endpoint security products either indefinitely or during a cutover period. Fortunately, Defender for Endpoint and the endpoint security suite is modular and can be adopted in a systematic approach.

Onboarding devices effectively enables the endpoint detection and response capability of Microsoft Defender for Endpoint. After onboarding the devices, you'll then need to configure the other capabilities of the service. The following table lists the capabilities you can configure to get the best protection for your environment and the order Microsoft recommends for how the endpoint security suite should be enabled.


| Capability | Description |Adoption Order Rank|
|---|---|---|
|[Endpoint Detection & Response (EDR)](overview-endpoint-detection-response.md)|Defender for Endpoint endpoint detection and response capabilities provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats. <p>|1|
| [Configure Microsoft Defender Vulnerability Management](/defender-vulnerability-management/tvm-prerequisites) | Defender Vulnerability Management is a component of Microsoft Defender for Endpoint, and provides both security administrators and security operations teams with unique value, including: <br><br> - Real-time endpoint detection and response (EDR) insights correlated with endpoint vulnerabilities. <br><br> - Invaluable device vulnerability context during incident investigations. <br><br> - Built-in remediation processes through Microsoft Intune and Microsoft System Center Configuration Manager.|2|
| [Configure Next-generation protection (NGP)](configure-microsoft-defender-antivirus-features.md) | Microsoft Defender Antivirus is a built-in antimalware solution that provides next-generation protection for desktops, portable computers, and servers. Microsoft Defender Antivirus includes:<br> <br>-Cloud-delivered protection for near-instant detection and blocking of new and emerging threats. Along with machine learning and the Intelligent Security Graph, cloud-delivered protection is part of the next-gen technologies that power Microsoft Defender Antivirus.<br> <br> - Always-on scanning using advanced file and process behavior monitoring and other heuristics (also known as "real-time protection").<br><br> - Dedicated protection updates based on machine learning, human and automated big-data analysis, and in-depth threat resistance research. |3|
| [Configure attack surface reduction](overview-attack-surface-reduction.md) | Attack surface reduction capabilities in Microsoft Defender for Endpoint help protect the devices and applications in the organization from new and emerging threats. |4|
| [Configure Auto Investigation & Remediation (AIR) capabilities](configure-automated-investigations-remediation.md) | Microsoft Defender for Endpoint uses Automated investigations to significantly reduce the volume of alerts that need to be investigated individually. The Automated investigation feature uses various inspection algorithms, and processes used by analysts (such as playbooks) to examine alerts and take immediate remediation action to resolve breaches. AIR significantly reduces alert volume, allowing security operations experts to focus on more sophisticated threats and other high value initiatives.|Not applicable|
| [Activate Microsoft Defender for Identity capabilities directly on a domain controller](/defender-for-identity/deploy/activate-capabilities) | Microsoft Defender for Identity customers, who've already onboarded their domain controllers to Defender for Endpoint, can activate Microsoft Defender for Identity capabilities directly on a domain controller instead of using a Microsoft Defender for Identity sensor. |Not applicable|
| [Configure Microsoft Defender Experts capabilities](/defender-xdr/defender-experts-for-hunting) | Microsoft  Experts is a managed hunting service that provides Security Operation Centers (SOCs) with expert level monitoring and analysis to help them ensure that critical threats in their unique environments don't get missed.|Not applicable|

For more information, see [Supported Microsoft Defender for Endpoint capabilities by platform](supported-capabilities-by-platform.md).
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
