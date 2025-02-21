---
title: Investigate entities on devices using live response in Microsoft Defender for Endpoint
description: Access a device using a secure remote shell connection to do investigative work and take immediate response actions on a device in real time.
ms.service: defender-endpoint
ms.author: diannegali
author: diannegali
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
- mde-edr
ms.topic: conceptual
ms.subservice: edr
search.appverid: met150
ms.date: 02/04/2025
---

# Investigate entities on devices using live response

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

Live response gives security operations teams instantaneous access to a device (also referred to as a machine) using a remote shell connection. Live response gives you the power to do in-depth investigative work and take immediate response actions to promptly contain identified threats in real time.

Live response is designed to enhance investigations by enabling your security operations team to collect forensic data, run scripts, send suspicious entities for analysis, remediate threats, and proactively hunt for emerging threats.

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=38c8abec-021a-4cda-9198-5ff6402a79ee]

With live response, analysts can do all of the following tasks:

- Run basic and advanced commands to do investigative work on a device.
- Download files such as malware samples and outcomes of PowerShell scripts.
- Download files in the background (new!).
- Upload a PowerShell script or executable to the library and run it on a device from a tenant level.
- Take or undo remediation actions.

## Before you begin

Before you can initiate a session on a device, make sure you fulfill the following requirements:

- **Verify that you're running a supported version of Windows**.

  Devices must be running one of the following versions of Windows

  - **Windows 10 & 11**
    - [Version 1909](/windows/whats-new/whats-new-windows-10-version-1909) or later
    - [Version 1903](/windows/whats-new/whats-new-windows-10-version-1903) with [KB4515384](https://support.microsoft.com/help/4515384/windows-10-update-kb4515384)
    - [Version 1809 (RS 5)](/windows/whats-new/whats-new-windows-10-version-1809) with [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818)
    - [Version 1803 (RS 4)](/windows/whats-new/whats-new-windows-10-version-1803) with [KB4537795](https://support.microsoft.com/help/4537795/windows-10-update-kb4537795)
    - [Version 1709 (RS 3)](/windows/whats-new/whats-new-windows-10-version-1709) with [KB4537816](https://support.microsoft.com/help/4537816/windows-10-update-kb4537816)

  - **macOS** - Minimum required version: 101.43.84. Supported for Intel-based and ARM-based macOS devices.

  - **Linux** - Minimum required version: 101.45.13

  - **Windows Server 2012 R2** - with [KB5005292](https://support.microsoft.com/topic/microsoft-defender-for-endpoint-update-for-edr-sensor-f8f69773-f17f-420f-91f4-a8e5167284ac)

  - **Windows Server 2016** - with [KB5005292](https://support.microsoft.com/topic/microsoft-defender-for-endpoint-update-for-edr-sensor-f8f69773-f17f-420f-91f4-a8e5167284ac)

    > [!NOTE]
    > For Windows Server 2012 R2 or Windows Server 2016, you must have the [Unified Agent](update-agent-mma-windows.md#update-mma-on-your-devices) installed, and it is recommended to patch to latest sensor version with KB5005292. Live response doesn't work as expected for offline down-level servers onboarded using the streamlined method, because of the static proxy. Consider using a system proxy instead.
    
  - **Windows Server 2019**
    - Version 1903 or (with [KB4515384](https://support.microsoft.com/help/4515384/windows-10-update-kb4515384)) later
    - Version 1809 (with [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818))

  - **Windows Server 2022**

  - **Windows Server 2025** (beginning in February 2025 and rolling out over the next several weeks)

- **Enable live response from the advanced settings page**.

  You need to enable the live response capability in the [Advanced features settings](advanced-features.md) page.

  > [!NOTE]
  > Only admins and users who have "Manage Portal Settings" permissions can enable live response.

- **Enable live response for servers from the advanced settings page** (recommended).

  > [!NOTE]
  > Only admins and users who have "Manage Portal Settings" permissions can enable live response.

- **Enable live response unsigned script execution** (optional).

  > [!IMPORTANT]
  > Signature verification only applies for PowerShell scripts.

  > [!WARNING]
  > Allowing the use of unsigned scripts may increase your exposure to threats.

  Running unsigned scripts isn't recommended as it can increase your exposure to threats. If you must use them however, you need to enable the setting in the [Advanced features settings](advanced-features.md) page.

- **Ensure that you have the appropriate permissions**.

  Only users who are provisioned with the appropriate permissions can initiate a session. For more information on role assignments, see [Create and manage roles](user-roles.md).

  > [!IMPORTANT]
  > The option to upload a file to the library is only available to users with "Manage Security Settings" permission.
  > The button is greyed out for users with only delegated permissions.

  Depending on the role that's been granted to you, you can run basic or advanced live response commands. Users permissions are controlled by RBAC custom role.

## Live response dashboard overview

When you initiate a live response session on a device, a dashboard opens. The dashboard provides information about the session such as the following:

- Who created the session
- When the session started
- The duration of the session

The dashboard also gives you access to:

- Disconnect session
- Upload files to the library
- Command console
- Command log

## Initiate a live response session on a device

> [!NOTE]
> Live response actions initiated from the Device page are not available in the MachineActions API.

1. Sign in to [Microsoft Defender portal](https://security.microsoft.com).

2. Navigate to **Endpoints** > **Device inventory** and select a device to investigate. The devices page opens.

3. Launch the live response session by selecting **Initiate live response session**. A command console is displayed. Wait while the session connects to the device.

4. Use the built-in commands to do investigative work. For more information, see [Live response commands](#live-response-commands).

5. After completing your investigation, select **Disconnect session**, then select **Confirm**.

## Live response commands

Depending on the role that's been granted to you, you can run basic or advanced live response commands. User permissions are controlled by RBAC custom roles. For more information on role assignments, see [Create and manage roles](user-roles.md).

> [!NOTE]
> Live response is a cloud-based interactive shell, as such, specific command experience may vary in response time depending on network quality and system load between the end user and the target device.

### Basic commands

The following commands are available for user roles that are granted the ability to run **basic** live response commands. For more information on role assignments, see [Create and manage roles](user-roles.md).

| Command  | Description  | Windows and Windows Server  | macOS  | Linux  |
|---|---|---|---|---|
| `cd`  | Changes the current directory.  | Y  | Y  | Y  |
| `cls`  | Clears the console screen.  | Y  | Y  | Y  |
| `connect`  | Initiates a live response session to the device.  | Y  | Y  | Y  |
| `connections`  | Shows all the active connections.  | Y  | N  | N  |
| `dir`  | Shows a list of files and subdirectories in a directory.  | Y  | Y  | Y  |
| `drivers`  | Shows all drivers installed on the device.  | Y  | N  | N  |
| `fg <command ID>`  | Place the specified job in the foreground, making it the current job.  Note that `fg` takes a `command ID` available from jobs, not a PID.  | Y  | Y  | Y  |
| `fileinfo`  | Get information about a file.  | Y  | Y  | Y  |
| `findfile`  | Locates files by a given name on the device.  | Y  | Y  | Y  |
| `getfile <file_path>`  | Downloads a file.  | Y  | Y  | Y  |
| `help`  | Provides help information for live response commands.  | Y  | Y  | Y  |
| `jobs`  | Shows currently running jobs, their ID and status.  | Y  | Y  | Y  |
| `persistence`  | Shows all known persistence methods on the device.  | Y  | N  | N  |
| `processes`  | Shows all processes running on the device.  | Y  | Y  | Y  |
| `registry`  | Shows registry values.  | Y  | N  | N  |
| `scheduledtasks`  | Shows all scheduled tasks on the device.  | Y  | N  | N  |
| `services`  | Shows all services on the device.  | Y  | N  | N  |
| `startupfolders`  | Shows all known files in startup folders on the device.  | Y  | N  | N  |
| `status`  | Shows the status and output of specific command.  | Y  | Y  | Y  |
| `trace`  | Sets the terminal's logging mode to debug.  | Y  | Y  | Y  |

### Advanced commands

The following commands are available for user roles that are granted the ability to run **advanced** live response commands. For more information on role assignments, see [Create and manage roles](user-roles.md).

| Command  | Description  | Windows and Windows Server  | macOS  | Linux  |
|---|---|---|---|---|
| `analyze`  | Analyses the entity with various incrimination engines to reach a verdict.  | Y  | N  | N  |
| `collect`  | Collects forensics package from device.  | N  | Y  | Y  |
| `isolate`  | Disconnects the device from the network while retaining connectivity to the Defender for Endpoint service.  | N  | Y  | N  |
| `release`  | Releases a device from network isolation.  | N  | Y  | N  |
| `run`  | Runs a PowerShell script from the library on the device.  | Y  | Y  | Y  |
| `library`  | Lists files that were uploaded to the live response library.  | Y  | Y  | Y  |
| `putfile`  | Puts a file from the library to the device. Files are saved in a working folder and are deleted when the device restarts by default.  | Y  | Y  | Y  |
| `remediate`  | Remediates an entity on the device. The remediation action varies, depending on the entity type: <br/>- File: delete<br/>- Process: stop, delete image file<br/>- Service: stop, delete image file<br/>- Registry entry: delete<br/>- Scheduled task: remove<br/>- Startup folder item: delete file<br/><br/>This command has a prerequisite command. You can use the `-auto` command in conjunction with remediate to automatically run the prerequisite command.  | Y  | Y  | Y  |
| `scan` | Runs a quick antivirus scan to help identify and remediate malware. | N | Y | Y |
| `undo`  | Restores an entity that was remediated.  | Y  | N  | N  |

> [!NOTE]
> The following file size limits apply for `putfile` live response command:
>
> - Windows: 300 MB
> - Other platforms: 10 MB


## Use live response commands

The commands that you can use in the console follow similar principles as [Windows Commands](/windows-server/administration/windows-commands/windows-commands#BKMK_c).

The advanced commands offer a more robust set of actions that allow you to take more powerful actions such as download and upload a file, run scripts on the device, and take remediation actions on an entity.

### Get a file from the device

For scenarios when you'd like get a file from a device you're investigating, you can use the `getfile` command. This allows you to save the file from the device for further investigation.

> [!NOTE]
> The following file size limits apply:
>
> - `getfile` limit: 3 GB
> - `fileinfo` limit: 30 GB
> - `library` limit: 250 MB

### Download a file in the background

To enable your security operations team to continue investigating an impacted device, files can now be downloaded in the background.

- To download a file in the background, in the live response command console, type `download <file_path> &`.
- If you are waiting for a file to be downloaded, you can move it to the background by using Ctrl + Z.
- To bring a file download to the foreground, in the live response command console, type `fg <command_id>`.

Here are some examples:

|Command|What it does|
|---|---|
|`getfile "C:\windows\some_file.exe" &`|Starts downloading a file named *some_file.exe* in the background.|
|`fg 1234`|Returns a download with command ID *1234* to the foreground.|
|

### Put a file in the library

Live response has a library where you can put files into. The library stores files (such as scripts) that can be run in a live response session at the tenant level.

Live response allows PowerShell and Bash scripts to run; however, you must first put the files into the library before you can run them.

You can have a collection of PowerShell and Bash scripts that can run on devices that you initiate live response sessions with.

#### To upload a file in the library

> [!NOTE]
> There are restrictions on the characters that can be uploaded to the library. Use alphanumeric characters and some symbols (specifically, `-`, `_`, or `.`).

1. Select **Upload file to library**.

2. Select **Browse** and select the file.

3. Provide a brief description.

4. Specify if you'd like to overwrite a file with the same name.

5. If you'd like to be,  know what parameters are needed for the script, select the script parameters check box. In the text field, enter an example and a description.

6. Select **Confirm**.

7. (Optional) To verify that the file was uploaded to the library, run the `library` command.

### Cancel a command

Anytime during a session, you can cancel a command by pressing CTRL + C.

> [!WARNING]
> Using this shortcut doesn't stop the command in the agent side. It only cancels the command in the Microsoft Defender portal. So, changing operations such as "remediate" may continue, even if the command is canceled.

## Run a script

Before you can run a PowerShell/Bash script, you must first upload it to the library.

After uploading the script to the library, use the `run` command to run the script.

If you plan to use an unsigned PowerShell script in the session, you'll need to enable the setting in the [Advanced features settings](advanced-features.md) page.

> [!WARNING]
> Allowing the use of unsigned scripts may increase your exposure to threats.

## Apply command parameters

- View the console help to learn about command parameters. To learn about an individual command, run:

  ```powershell
  help <command name>
  ```

- When applying parameters to commands, note that parameters are handled based on a fixed order:

  ```powershell
  <command name> param1 param2
  ```

- When specifying parameters outside of the fixed order, specify the name of the parameter with a hyphen before providing the value:

  ```powershell
  <command name> -param2_name param2
  ```

- When using commands that have prerequisite commands, you can use flags:

  ```powershell
  <command name> -type file -id <file path> - auto
  ```

  or

  ```powershell
  remediate file <file path> - auto`
  ```

## Supported output types

Live response supports table and JSON format output types. For each command, there's a default output behavior. You can modify the output in your preferred output format using the following commands:

- `-output json`
- `-output table`

> [!NOTE]
> Fewer fields are shown in table format due to the limited space. To see more details in the output, you can use the JSON output command so that more details are shown.

## Supported output pipes

Live response supports output piping to CLI and file. CLI is the default output behavior. You can pipe the output to a file using the following command: `[command] > [filename].txt`.

Example:

```console
processes > output.txt
```

## View the command log

Select the **Command log** tab to see the commands used on the device during a session. Each command is tracked with full details such as:

- ID
- Command line
- Duration
- Status and input or output side bar

## Limitations

- Live response sessions are limited to 25 live response sessions at a time.
- Live response session inactive timeout value is 30 minutes.
- Individual live response commands have a time limit of 10 minutes, with the exception of `getfile`, `findfile`, and `run`, which have a limit of 30 minutes.
- A user can initiate up to 10 concurrent sessions.
- A device can only be in one session at a time.
- The following file size limits apply:
  - `getfile` limit: 3 GB
  - `fileinfo` limit: 30 GB
  - `library` limit: 250 MB

## Related article

- [Live response command examples](live-response-command-examples.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
