---
title: Schedule regular quick and full scans with Microsoft Defender Antivirus
description: Set up recurring (scheduled) scans, including when they should run and whether they run as full or quick scans
ms.service: defender-endpoint
ms.localizationpriority: medium
author: emmwalshh
ms.author: ewalsh
ms.custom: nextgen
ms.date: 02/05/2025
ms.reviewer: pauhijbr, ksarens, yongrhee, bsabetghadam
manager: deniseb
ms.subservice: ngp
ms.topic: how-to
ms.collection: 
- m365-security
- tier3
- mde-ngp
search.appverid: met150
---

# Configure scheduled quick or full Microsoft Defender Antivirus scans

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- Microsoft Defender Antivirus

**Platforms**
- Windows

You can set up regular, scheduled antivirus scans on devices. These scheduled scans are in addition to always-on, real-time protection and [on-demand antivirus](run-scan-microsoft-defender-antivirus.md) scans. When you schedule a scan, you can specify the type of scan, when the scan should occur, and if the scan should occur after a [protection update](manage-protection-updates-microsoft-defender-antivirus.md) or when a device isn't being used. You can also set up special scans to complete remediation actions if needed.

## Comparing the quick scan, full scan, and custom scan

The following table describes the different types of scans you can configure. For more information, see [Microsoft Defender Antivirus scan considerations and best practices](mdav-scan-best-practices.md).

| Scan type | Description |
|:---|:---|
| Quick scan <br/>(*recommended*) | A quick scan looks at all the locations where there could be malware registered to start with the system, such as registry keys and known Windows startup folders. Quick scans also run on mounted removable devices, such as USB drives. <br/><br/>A quick scan helps provide strong protection against malware that starts with the system and kernel-level malware, together with [always-on real-time protection](configure-real-time-protection-microsoft-defender-antivirus.md), which reviews files when they're opened and closed, and whenever a user navigates to a folder.<br/><br/>Preview: In most cases, a quick scan is sufficient and is the recommended option for scheduled scans. Starting with the December 2023 (4.18.2311.x.x) release of [Platform Update](microsoft-defender-antivirus-updates.md), you have the option named "Quick scan include exclusions" to scan all files and directories that are excluded from real-time protection that is using contextual exclusions.  By enabling this policy, the excluded files and folders are scanned during a quick scan.  Note:  While in preview, management is available in Intune - Settings Catalog.|
| Full scan | A full scan begins with a quick scan and then scans all mounted fixed disks and removable/network drives (if the full scan is configured to do so).<br/><br/>A full scan can take a few hours or days to complete, depending on the amount and type of data that needs to be scanned.<br/><br/> The full scan uses the security intelligence definitions installed at the time the scan starts. If new updates are released during the full scan, another full scan is required in order to scan for new threat detections contained in the latest update.<br/><br/> Due to the time and resources involved, we generally don't recommend scheduling full scans.|
| Custom scan | A custom scan runs on files and folders that you specify. For example, you can choose to scan a USB drive or a specific folder on your device's local drive.|

> [!TIP]
> If you have a Network-Attached Storage (NAS) or Storage Area Network (SAN), you can use Internet Content Adaption Protocol (ICAP) scanning with the Microsoft Defender Antivirus engine. For more information, see [Tech Community Blog: MetaDefender ICAP with Windows Defender Antivirus: World-class security for hybrid environments](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/metadefender-icap-with-windows-defender-antivirus-world-class/ba-p/800234).   

## How to choose a scan type

Use the following table to choose a scan type. Also see [Microsoft Defender Antivirus scan considerations and best practices](mdav-scan-best-practices.md).

|Scenario|Recommended scan type|
|---|---|
|You want to set up regular, scheduled scans|Quick scan <br/><br/> A quick scan checks the processes, memory, profiles, and certain locations on the device. Together with [always-on real-time protection](configure-real-time-protection-microsoft-defender-antivirus.md), a quick scan helps provide strong coverage both for malware that starts with the system and kernel-level malware. Real-time protection reviews files when they're opened and closed, and whenever a user navigates to a folder.|
|Threats, such as malware, are detected on an individual device|Quick scan <br/><br/> In most cases, a quick scan will catch and clean up detected malware.|
|You want to run an [on-demand scan](run-scan-microsoft-defender-antivirus.md)|Quick scan|
|You want to make sure a portable device, such as a USB drive, doesn't contain malware|Custom scan <br/><br/> A custom scan enables you to select specific locations, folders, or files, and runs a quick scan.|
| You have installed or re-enabled Microsoft Defender Antivirus | Quick scan or full scan <br/><br/>A quick scan checks the processes, memory, profiles, and certain locations on the device. If you prefer, you can choose to run a full scan after you have enabled or installed Microsoft Defender Antivirus. Just keep in mind it can take a while to run a full scan. |

## Important points to keep in mind

- By default, Microsoft Defender Antivirus checks for an update 15 minutes before the time of any scheduled scans. You can [manage the schedule for when protection updates should be downloaded and applied](manage-protection-update-schedule-microsoft-defender-antivirus.md) to override this default.

- If a device is unplugged and running on battery during a scheduled full scan, the scheduled scan stops with event 1002, which states that the scan stopped before completion. Microsoft Defender Antivirus runs a full scan at the next scheduled time.

- Scheduled scans run according to the local time zone of the device.

- Malicious files can be stored in locations that aren't included in a quick scan. However, [always-on, real-time protection](configure-protection-features-microsoft-defender-antivirus.md) reviews all files that are opened & closed, and any files that are in folders that are accessed by a user. The combination of real-time protection and a quick scan helps provide strong protection against malware.

- On-access protection with [cloud-delivered protection](cloud-protection-microsoft-defender-antivirus.md) helps ensure that all the files accessed on the system are being scanned with the latest security intelligence and cloud machine learning models.

- When real-time protection detects malware and the extent of the affected files isn't determined initially, Microsoft Defender Antivirus initiates a full scan as part of the remediation process.

- If a device is offline for an extended period of time, a full scan can take longer to complete.

- You can configure quick scans to scan real-time protection exclusions by using PowerShell, Intune, or Group Policy.

## Scheduled quick scan performance optimization 

As a performance optimization, Microsoft Defender Antivirus skips running scheduled quick scans in some situations. This optimization only applies to a quick scan when initiated by a schedule – it doesn't affect a quick scan initiated by an [on-demand antivirus](run-scan-microsoft-defender-antivirus.md) scan. This optimization reduces performance degradation by avoiding running a quick scan when it isn't necessary and won't affect protection.

By default, if a qualified quick scan ran within the last seven days, a new quick scan won't be initiated. A quick scan is considered to be *qualified* if:

- The scan occurs after the last [Security Intelligence Update](microsoft-defender-antivirus-updates.md) was installed; 
- [Real-time protection](configure-protection-features-microsoft-defender-antivirus.md) wasn't disabled during that time period; and, 
- The machine was rebooted.  

This optimization *doesn't* apply to the following conditions: 

- If Microsoft Defender for Endpoint is [Managed](configuration-management-reference-microsoft-defender-antivirus.md)  
- If Microsoft Defender [Endpoint Detection and Response (EDR)](overview-endpoint-detection-response.md) is installed 
- If the computer was restarted since the last quick scan
- If [real-time protection](configure-real-time-protection-microsoft-defender-antivirus.md) is disabled after the last quick scan occurred 
- If the last initiated quick scan wasn't completed

This optimization applies to machines running Windows 10 Anniversary Update (version 1607) and all subsequent Windows releases, as well as Windows Server 2016 (version 1607) and subsequent Windows Server releases, but doesn't apply to Core Server installations.  

## See also

- [Microsoft Defender Antivirus scan considerations and best practices](mdav-scan-best-practices.md)
- [Exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md)
- [Onboard non-Windows devices](configure-endpoints-non-windows.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
