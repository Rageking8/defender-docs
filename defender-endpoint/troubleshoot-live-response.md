---
title: Troubleshoot Microsoft Defender for Endpoint live response issues
description: Troubleshoot issues that might arise when using live response in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
- mde-edr
ms.topic: troubleshooting
ms.subservice: edr
search.appverid: met150
ms.date: 02/16/2024
---

# Troubleshoot Microsoft Defender for Endpoint live response issues

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

This page provides detailed steps to troubleshoot live response issues.

## File can't be accessed during live response sessions

If while trying to take an action during a live response session, you encounter an error message stating that the file can't be accessed, take the following steps to address the issue.

1. Copy the following script code snippet and save it as a PS1 file:

    ```powershell
    $copied_file_path=$args[0]
    $action=Copy-Item $copied_file_path -Destination $env:TEMP -PassThru -ErrorAction silentlyContinue

    if ($action){
         Write-Host "You copied the file specified in $copied_file_path to $env:TEMP Successfully"
    }

    else{
        Write-Output "Error occurred while trying to copy a file, details:"
        Write-Output  $error[0].exception.message

    }
    ```

2. Add the script to the live response library.
3. Run the script with one parameter: the file path of the file to be copied.
4. Navigate to your TEMP folder.
5. Run the action you wanted to take on the copied file.

## Slow live response sessions or delays during initial connections

Live response uses Defender for Endpoint sensor registration with WNS service in Windows. If you're having connectivity issues with live response, confirm the following details:

1. WpnService (Windows Push Notifications System Service) isn't disabled.

2. WpnService connectivity with WNS cloud isn't disabled via group policy or MDM setting. ['Turn off notifications network usage'](/windows/client-management/mdm/policy-csp-notifications) shouldn't be set to `1`.

Refer to the following articles to fully understand the WpnService service behavior and requirements:

- [Windows Push Notification Services (WNS) overview](/windows/uwp/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)
- [Enterprise Firewall and Proxy Configurations to Support WNS Traffic](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config)
- [Microsoft Push Notifications Service (MPNS) Public IP ranges](https://www.microsoft.com/download/details.aspx?id=44535)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
