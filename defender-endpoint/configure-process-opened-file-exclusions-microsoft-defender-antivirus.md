---
title: Configure exclusions for files opened by specific processes
description: You can exclude files from scans if they've been opened by a specific process.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: emmwalshh
ms.author: ewalsh
ms.topic: conceptual
ms.custom: nextgen
ms.reviewer: yongrhee
manager: deniseb
ms.collection: 
- m365-security
- tier2
- mde-ngp
search.appverid: met150
ms.date: 03/19/2024
---



# Configure exclusions for files opened by processes

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- Microsoft Defender Antivirus

**Platforms**
- Windows 

You can exclude files that are opened by specific processes from Microsoft Defender Antivirus scans. These types of exclusions are for files that are opened by processes and not the processes themselves. To exclude a process, add a file exclusion (see [Configure and validate exclusions based on file extension and folder location](configure-extension-file-exclusions-microsoft-defender-antivirus.md)).

See [Important points about exclusions](configure-exclusions-microsoft-defender-antivirus.md#important-points-about-exclusions) and review the information in [Manage exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md) before defining your exclusion lists.

This article describes how to configure exclusion lists.

## Examples of process exclusions

|Exclusion|Example|
|---|---|
|Any file on the machine that is opened by any process with a specific file name|Specifying `test.exe` would exclude files opened by: <p>`c:\sample\test.exe` <p> `d:\internal\files\test.exe`|
|Any file on the machine that is opened by any process under a specific folder|Specifying `c:\test\sample\*` would exclude files opened by: <p> `c:\test\sample\test.exe` <p> `c:\test\sample\test2.exe` <p> `c:\test\sample\utility.exe`|
|Any file on the machine that is opened by a specific process in a specific folder|Specifying `c:\test\process.exe` would exclude files only opened by `c:\test\process.exe`|

When you add a process to the process exclusion list, Microsoft Defender Antivirus won't scan files opened by that process, no matter where the files are located. The process itself, however, will be scanned unless it has also been added to the [file exclusion list](configure-extension-file-exclusions-microsoft-defender-antivirus.md).

The exclusions only apply to [always-on real-time protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus.md). They don't apply to scheduled or on-demand scans.

Changes made with Group Policy to the exclusion lists **will show** in the lists in the [Windows Security app](microsoft-defender-security-center-antivirus.md). However, changes made in the Windows Security app **will not show** in the Group Policy lists.

You can add, remove, and review the lists for exclusions in Group Policy, Microsoft Configuration Manager, Microsoft Intune, and with the Windows Security app, and you can use wildcards to further customize the lists.

You can also use PowerShell cmdlets and WMI to configure the exclusion lists, including reviewing your lists.

By default, local changes made to the lists (by users with administrator privileges; changes made with PowerShell and WMI) are merged with the lists as defined (and deployed) by Group Policy, Configuration Manager, or Intune. The Group Policy lists take precedence if there are conflicts.

You can [configure how locally and globally defined exclusions lists are merged](configure-local-policy-overrides-microsoft-defender-antivirus.md#merge-lists) to allow local changes to override managed deployment settings.
    
> [!NOTE]
> **Network Protection** and **Attack surface reduction rules** are directly impacted by process exclusions on all platforms, meaning that a process exclusion on any OS (Windows, MacOS, Linux) will result in Network Protection or ASR being unable to inspect traffic or enforce rules for that specific process.

### Image name vs full path for process exclusions

Two different types of process exclusions may be set. A process may be excluded by image name, or by full path. The image name is simply the file name of the process, without the path.

For example, given the process `MyProcess.exe` running from `C:\MyFolder\` the full path to this process would be `C:\MyFolder\MyProcess.exe` and the image name is `MyProcess.exe`. 

Image name exclusions are much more broad - an exclusion on `MyProcess.exe` excludes any processes with this image name, regardless of the path they're run from. So for example, if the process `MyProcess.exe` is excluded by image name, it will also be excluded if it is run from `C:\MyOtherFolder`, from removable media, et cetera. As such it's recommended that whenever possible, the full path is used. 

### Use wildcards in the process exclusion list

The use of wildcards in the process exclusion list is different from their use in other exclusion lists. When the process exclusion is defined as an image name only, wildcard usage isn't allowed. However when a full path is used, wildcards are supported and the wildcard behavior behaves as described in [File and Folder Exclusions](configure-extension-file-exclusions-microsoft-defender-antivirus.md)

The use of environment variables (such as `%ALLUSERSPROFILE%`) as wildcards when defining items in the process exclusion list is also supported. Details and a full list of supported environment variables are described in [File and Folder Exclusions](configure-extension-file-exclusions-microsoft-defender-antivirus.md). 

The following table describes how the wildcards can be used in the process exclusion list, when a path is supplied:

|Wildcard|Example use|Example matches|
|---|---|---|
|`*` (asterisk) <p> Replaces any number of characters.|`C:\MyFolder\*`|Any file opened by `C:\MyFolder\MyProcess.exe` or `C:\MyFolder\AnotherProcess.exe`|
|                                                     |`C:\*\*\MyProcess.exe`|Any file opened by `C:\MyFolder1\MyFolder2\MyProcess.exe` or `C:\MyFolder3\MyFolder4\MyProcess.exe`|
|                                                     |`C:\*\MyFolder\My*.exe`|Any file opened by `C:\MyOtherFolder\MyFolder\MyProcess.exe` or `C:\AnotherFolder\MyFolder\MyOtherProcess.exe`|
|'?' (question mark) <p> Replaces one character.      |`C:\MyFolder\MyProcess??.exe`|Any file opened by `C:\MyFolder\MyProcess42.exe` or `C:\MyFolder\MyProcessAA.exe` or `C:\MyFolder\MyProcessF5.exe`|
| Environment Variables                                |`%ALLUSERSPROFILE%\MyFolder\MyProcess.exe`|Any file opened by `C:\ProgramData\MyFolder\MyProcess.exe`|

### Contextual Process Exclusions

A process exclusion may also be defined via a [Contextual exclusion](configure-contextual-file-folder-exclusions-microsoft-defender-antivirus.md) allowing, for example, a specific file to be excluded only if it's opened by a specific process. 

## Configure the list of exclusions for files opened by specified processes

### Use Microsoft Intune to exclude files that have been opened by specified processes from scans

For more information, see [Configure device restriction settings in Microsoft Intune](/mem/intune/configuration/device-restrictions-configure) and [Microsoft Defender Antivirus device restriction settings for Windows 10 in Intune](/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus).

### Use Microsoft Configuration Manager to exclude files that have been opened by specified processes from scans

See [How to create and deploy antimalware policies: Exclusion settings](/configmgr/protect/deploy-use/endpoint-antimalware-policies#exclusion-settings) for details on configuring Microsoft Configuration Manager (current branch).

### Use Group Policy to exclude files that have been opened by specified processes from scans

1. On your Group Policy management computer, open the [Group Policy Management Console](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731212(v=ws.11)), right-click the Group Policy Object you want to configure and click **Edit**.

2. In the **Group Policy Management Editor**, go to **Computer configuration** and click **Administrative templates**.

3. Expand the tree to **Windows components \> Microsoft Defender Antivirus \> Exclusions**.

4. Double-click **Process Exclusions** and add the exclusions:
    1. Set the option to **Enabled**.
    2. Under the **Options** section, click **Show...**.
    3. Enter each process on its own line under the **Value name** column. See the example table for the different types of process exclusions. Enter **0** in the **Value** column for all processes.

5. Click **OK**.

### Use PowerShell cmdlets to exclude files that have been opened by specified processes from scans

Using PowerShell to add or remove exclusions for files that have been opened by processes requires using a combination of three cmdlets with the `-ExclusionProcess` parameter. The cmdlets are all in the [Defender module](/powershell/module/defender/).

The format for the cmdlets is:

```PowerShell
<cmdlet> -ExclusionProcess "<item>"
```

The following are allowed as the \<cmdlet\>:

|Configuration action|PowerShell cmdlet|
|---|---|
|Create or overwrite the list|`Set-MpPreference`|
|Add to the list|`Add-MpPreference`|
|Remove items from the list|`Remove-MpPreference`|

> [!IMPORTANT]
> If you have created a list, either with `Set-MpPreference` or `Add-MpPreference`, using the `Set-MpPreference` cmdlet again overwrites the existing list.

For example, the following code snippet would cause Microsoft Defender Antivirus scans to exclude any file that is opened by the specified process:

```PowerShell
Add-MpPreference -ExclusionProcess "c:\internal\test.exe"
```

For more information on how to use PowerShell with Microsoft Defender Antivirus, see Manage antivirus with PowerShell cmdlets and [Microsoft Defender Antivirus cmdlets](/powershell/module/defender).

## Use Windows Management Instruction (WMI) to exclude files that have been opened by specified processes from scans

Use the [**Set**, **Add**, and **Remove** methods of the **MSFT_MpPreference**](/previous-versions/windows/desktop/legacy/dn455323(v=vs.85)) class for the following properties:

```WMI
ExclusionProcess
```

The use of **Set**, **Add**, and **Remove** is analogous to their counterparts in PowerShell: `Set-MpPreference`, `Add-MpPreference`, and `Remove-MpPreference`.

For more information and allowed parameters, see  [Windows Defender WMIv2 APIs](/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## Use the Windows Security app to exclude files that have been opened by specified processes from scans

Follow the instructions in [Add exclusions in the Windows Security app](microsoft-defender-security-center-antivirus.md).

## Review the list of exclusions

You can retrieve the items in the exclusion list with MpCmdRun, PowerShell, [Microsoft Configuration Manager](/mem/configmgr/protect/deploy-use/endpoint-antimalware-policies#exclusion-settings), [Intune](/mem/intune/configuration/device-restrictions-configure), or the [Windows Security app](microsoft-defender-security-center-antivirus.md).

If you use PowerShell, you can retrieve the list in two ways:

- Retrieve the status of all Microsoft Defender Antivirus preferences. Each of the lists is displayed on separate lines, but the items within each list are combined into the same line.
- Write the status of all preferences to a variable, and use that variable to only call the specific list you're interested in. Each use of `Add-MpPreference` is written to a new line.

### Validate the exclusion list by using MpCmdRun

To check exclusions with the dedicated [command-line tool mpcmdrun.exe](./command-line-arguments-microsoft-defender-antivirus.md?branch=v-anbic-wdav-new-mpcmdrun-options), use the following command:

```DOS
MpCmdRun.exe -CheckExclusion -path <path>
```

> [!NOTE]
> Checking exclusions with MpCmdRun requires Microsoft Defender Antivirus CAMP version 4.18.1812.3 (released in December 2018) or later.

### Review the list of exclusions alongside all other Microsoft Defender Antivirus preferences by using PowerShell

Use the following cmdlet:

```PowerShell
Get-MpPreference
```

For more information on how to use PowerShell with Microsoft Defender Antivirus, see [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus.md) and [Microsoft Defender Antivirus cmdlets](/powershell/module/defender) .

### Retrieve a specific exclusions list by using PowerShell

Use the following code snippet (enter each line as a separate command); replace **WDAVprefs** with whatever label you want to name the variable:

```PowerShell
$WDAVprefs = Get-MpPreference
$WDAVprefs.ExclusionProcess
```

For more information on how to use PowerShell with Microsoft Defender Antivirus, see [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus.md) and [Microsoft Defender Antivirus cmdlets](/powershell/module/defender).

> [!TIP]
> If you're looking for Antivirus related information for other platforms, see:
> - [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences.md)
> - [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac.md)
> - [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/mem/intune/protect/antivirus-microsoft-defender-settings-macos)
> - [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences.md)
> - [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux.md)
> - [Configure Defender for Endpoint on Android features](android-configure.md)
> - [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features.md)

## Related articles

- [Configure and validate exclusions in Microsoft Defender Antivirus scans](configure-exclusions-microsoft-defender-antivirus.md)
- [Configure and validate exclusions based on file name, extension, and folder location](configure-extension-file-exclusions-microsoft-defender-antivirus.md)
- [Configure Microsoft Defender Antivirus exclusions on Windows Server](configure-server-exclusions-microsoft-defender-antivirus.md)
- [Common mistakes to avoid when defining exclusions](common-exclusion-mistakes-microsoft-defender-antivirus.md)
- [Customize, initiate, and review the results of Microsoft Defender Antivirus scans and remediation](customize-run-review-remediate-scans-microsoft-defender-antivirus.md)
- [Microsoft Defender Antivirus in Windows 10](microsoft-defender-antivirus-windows.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
