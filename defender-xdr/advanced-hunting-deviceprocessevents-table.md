---
title: DeviceProcessEvents table in the advanced hunting schema
description: Learn about the process spawning or creation events in the DeviceProcessEventstable of the advanced hunting schema
search.appverid: met150
ms.service: defender-xdr
ms.subservice: adv-hunting
f1.keywords: 
  - NOCSH
ms.author: maccruz
author: schmurky
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.custom: 
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 09/06/2024
---

# DeviceProcessEvents

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]


**Applies to:**
- Microsoft Defender XDR
- Microsoft Defender for Endpoint



The `DeviceProcessEvents` table in the [advanced hunting](advanced-hunting-overview.md) schema contains information about process creation and related events. Use this reference to construct queries that return information from this table.

> [!TIP]
> For detailed information about the events types (`ActionType` values) supported by a table, use the built-in schema reference available in Microsoft Defender XDR.

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables.md).

| Column name | Data type | Description |
|-------------|-----------|-------------|
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `ActionType` | `string` | Type of activity that triggered the event. See the [in-portal schema reference](advanced-hunting-schema-tables.md?#get-schema-information-in-the-security-center) for details. |
| `FileName` | `string` | Name of the file that the recorded action was applied to |
| `FolderPath` | `string` | Folder containing the file that the recorded action was applied to |
| `SHA1` | `string` | SHA-1 of the file that the recorded action was applied to |
| `SHA256` | `string` | SHA-256 of the file that the recorded action was applied to. This field is usually not populated — use the SHA1 column when available. |
| `MD5` | `string` | MD5 hash of the file that the recorded action was applied to |
| `FileSize` | `long` | Size of the file in bytes |
| `ProcessVersionInfoCompanyName` | `string` | Company name from the version information of the newly created process |
| `ProcessVersionInfoProductName` | `string` | Product name from the version information of the newly created process |
| `ProcessVersionInfoProductVersion` | `string` | Product version from the version information of the newly created process |
| `ProcessVersionInfoInternalFileName` | `string` | Internal file name from the version information of the newly created process |
| `ProcessVersionInfoOriginalFileName` | `string` | Original file name from the version information of the newly created process |
| `ProcessVersionInfoFileDescription` | `string` | Description from the version information of the newly created process |
| `ProcessId` | `long` | Process ID (PID) of the newly created process |
| `ProcessCommandLine` | `string` | Command line used to create the new process |
| `ProcessIntegrityLevel` | `string` | Integrity level of the newly created process. Windows assigns integrity levels to processes based on certain characteristics, such as if they were launched from an internet downloaded. These integrity levels influence permissions to resources. |
| `ProcessTokenElevation` | `string` | Indicates the type of token elevation applied to the newly created process. Possible values: TokenElevationTypeLimited (restricted), TokenElevationTypeDefault (standard), and TokenElevationTypeFull (elevated) |
| `ProcessCreationTime` | `datetime` | Date and time the process was created |
| `AccountDomain` | `string` | Domain of the account |
| `AccountName` | `string` | User name of the account; if the device is registered in Microsoft Entra ID, the Entra ID user name of the account might be shown instead |
| `AccountSid` | `string` | Security Identifier (SID) of the account |
| `AccountUpn` | `string` | User principal name (UPN) of the account; if the device is registered in Microsoft Entra ID, the Entra ID UPN of the account might be shown instead |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `LogonId` | `long` | Identifier for a logon session. This identifier is unique on the same device only between restarts. |
| `InitiatingProcessAccountDomain` | `string` | Domain of the account that ran the process responsible for the event |
| `InitiatingProcessAccountName` | `string` | User name of the account that ran the process responsible for the event; if the device is registered in Microsoft Entra ID, the Entra ID user name of the account that ran the process responsible for the event might be shown instead |
| `InitiatingProcessAccountSid` | `string` | Security Identifier (SID) of the account that ran the process responsible for the event |
| `InitiatingProcessAccountUpn` | `string` | User principal name (UPN) of the account that ran the process responsible for the event; if the device is registered in Microsoft Entra ID, the Entra ID UPN of the account that ran the process responsible for the event might be shown instead |
| `InitiatingProcessAccountObjectId` | `string` | Microsoft Entra object ID of the user account that ran the process responsible for the event |
| `InitiatingProcessLogonId` | `long` | Identifier for a logon session of the process that initiated the event. This identifier is unique on the same device only between restarts. |
| `InitiatingProcessIntegrityLevel` | `string` | Integrity level of the process that initiated the event. Windows assigns integrity levels to processes based on certain characteristics, such as if they were launched from an internet download. These integrity levels influence permissions to resources. |
| `InitiatingProcessTokenElevation` | `string` | Token type indicating the presence or absence of User Access Control (UAC) privilege elevation applied to the process that initiated the event |
| `InitiatingProcessSHA1` | `string` | SHA-1 hash of the process (image file) that initiated the event |
| `InitiatingProcessSHA256` | `string` | SHA-256 of the process (image file) that initiated the event. This field is usually not populated — use the SHA1 column when available. |
| `InitiatingProcessMD5` | `string` | MD5 hash of the process (image file) that initiated the event |
| `InitiatingProcessFileName` | `string` | Name of the process file that initiated the event; if unavailable, the name of the process that initiated the event might be shown instead |
| `InitiatingProcessFileSize` | `long` | Size of the file that ran the process responsible for the event |
| `InitiatingProcessVersionInfoCompanyName` | `string` | Company name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoProductName` | `string` | Product name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoProductVersion` | `string` | Product version from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoInternalFileName` | `string` | Internal file name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoOriginalFileName` | `string` | Original file name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoFileDescription` | `string` | Description from the version information of the process (image file) responsible for the event |
| `InitiatingProcessId` | `long` | Process ID (PID) of the process that initiated the event |
| `InitiatingProcessCommandLine` | `string` | Command line used to run the process that initiated the event |
| `InitiatingProcessCreationTime` | `datetime` | Date and time when the process that initiated the event was started |
| `InitiatingProcessFolderPath` | `string` | Folder containing the process (image file) that initiated the event |
| `InitiatingProcessParentId` | `long` | Process ID (PID) of the parent process that spawned the process responsible for the event |
| `InitiatingProcessParentFileName` | `string` | Name of the parent process that spawned the process responsible for the event |
| `InitiatingProcessParentCreationTime` | `datetime` | Date and time when the parent of the process responsible for the event was started |
| `InitiatingProcessSignerType` | `string` | Type of file signer of the process (image file) that initiated the event |
| `InitiatingProcessSignatureStatus` | `string` | Information about the signature status of the process (image file) that initiated the event |
| `ReportId` | `long` | Event identifier based on a repeating counter. To identify unique events, this column must be used in conjunction with the DeviceName and Timestamp columns. |
| `AppGuardContainerId` | `string` | Identifier for the virtualized container used by Application Guard to isolate browser activity |
| `AdditionalFields` | `string` | Additional information about the event in JSON array format |
| `InitiatingProcessSessionId` | `long` |  Windows session ID of the initiating process  |
| `IsInitiatingProcessRemoteSession` | `bool` |   Indicates whether the initiating process was run under a remote desktop protocol (RDP) session (true) or locally (false) |
| `InitiatingProcessRemoteSessionDeviceName` | `string` | Device name of the remote device from which the initiating process's RDP session was initiated |
| `InitiatingProcessRemoteSessionIP` | `string` | IP address of the remote device from which the initiating process's RDP session was initiated |
| `CreatedProcessSessionId` | `long` | Windows session ID of the created process |
|`IsProcessRemoteSession` | `bool` | Indicates whether the created process was run under a remote desktop protocol (RDP) session (true) or locally (false) |
| `ProcessRemoteSessionDeviceName` | `string` | Device name of the remote device from which the created process's RDP session was initiated |
| `ProcessRemoteSessionIP` | `string` | IP address of the remote device from which the created process's RDP session was initiated |


## Related topics
- [Advanced hunting overview](advanced-hunting-overview.md)
- [Learn the query language](advanced-hunting-query-language.md)
- [Use shared queries](advanced-hunting-shared-queries.md)
- [Hunt across devices, emails, apps, and identities](advanced-hunting-query-emails-devices.md)
- [Understand the schema](advanced-hunting-schema-tables.md)
- [Apply query best practices](advanced-hunting-best-practices.md)
[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
