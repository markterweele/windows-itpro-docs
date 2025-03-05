---
title: Configure a Kiosk With Shell Launcher
description: Learn how to configure a Windows kiosk with Shell Launcher.
ms.date: 02/27/2025
ms.topic: how-to
---

# Configure a kiosk with Shell Launcher

There are two ways you can configure Shell Launcher:

1. Using the `ShellLauncher` node of the [Assigned Access Configuration Service Provider (CSP)](/windows/client-management/mdm/assignedaccess-csp), which also automatically enables Shell Launcher on the device, if the device supports it
1. Using the **Shell Launcher WMI providers** directly in an application. When using this method, you must [enable Shell Launcher](enable.md) first

You can configure the following options for Shell Launcher:

- Enable or disable Shell Launcher
- Specify a shell configuration for a specific user or group
- Remove a shell configuration for a specific user or group
- Change the default shell configuration
- Get information on a shell configuration for a specific user or group

Any changes don't take effect until a user signs in.

## Launch different shells for different user accounts

By default, Shell Launcher runs the default shell, which is specified when you create the OS image at design time. The default shell is set to Cmd.exe, but you can specify any executable file to be the default shell.

You can configure Shell Launcher to launch a different shell for specific users or groups if you don't want to run the default shell. For example, you might configure a device to run a custom application shell for guest accounts, but run the standard Windows Explorer shell for administrator accounts in order to service the device.

If you use the WMI providers to configure Shell Launcher for a user or group at run time, you must use the security identifier (SID) for that user or group; you can't use the user name or group name.

For more information about common security identifiers, see [Well-known SIDs](/windows/win32/secauthz/well-known-sids).

When the current signed in account belongs to two or more groups that have different configurations defined for each group, Shell Launcher uses the first configuration it finds. The search order isn't defined, so we recommend that you avoid assigning a user to multiple groups with different Shell Launcher configurations.

## Perform an action when the shell exits

When a custom shell exits, Shell Launcher can perform one of four actions:

|Action|Description|
|:---:|:---|
|`0`|Restart the shell.|
|`1`|Restart the device.|
|`2`|Shut down the device.|
|`3`|Do nothing.|

> [!IMPORTANT]
> Make sure that your shell application does not automatically exit and is not automatically closed by any features such as Dialog Filter, as this can lead to an infinite cycle of exiting and restarting, unless the return code action is set to do nothing.

### Default return code action

You can define a default return code action for Shell Launcher with the DefaultReturnCodeAction setting. If you don't change the initial value, the default return code action is set to 0 (zero), which indicates that Shell Launcher restarts the shell when the shell exits.

### Map the exit code to a Shell Launcher action

Shell Launcher can take a specific action based on the exit code returned by the shell. For any given exit code returned by the shell, you can configure the action that Shell Launcher takes by mapping that exit code to one of the shell exit actions.

If the exit code doesn't match a defined value, Shell Launcher performs the default return code action.

For example, your shell might return exit code values of `-1`, `0`, `1`, or `255` depending on how the shell exits. You can configure Shell Launcher to:

- restart the device (`1`) when the shell returns an exit code of value `-1`
- restart the shell (`0`) when the shell returns an exit code of value `0`
- do nothing (`3`) when the shell returns an exit code of value 1
- shut down the device (`2`) when the shell returns an exit code of value `255`

Your custom return code action mapping would look like this:

|Exit code|Action|
|:----:|----|
|`-1`|`1` (restart the device)|
|`0`|`0` (restart the shell)|
|`1`|`3` (do nothing)|
|`255`|`2` (shut down the device)|

## Set your custom shell with the Assigned Access CSP

The configuration of Shell Launcher is done using an XML file. The XML file is applied to the device via the [Assigned Access CSP](/windows/client-management/mdm/assignedaccess-csp#shelllauncher), using one of the following options:

- A Mobile Device Management (MDM) solution, like Microsoft Intune
- Provisioning packages
- The MDM Bridge WMI Provider

> [!NOTE]
> Configuring Shell Launcher using Assigned Access CSP, automatically enables Shell Launcher on the device, if the device supports it.

To learn how to configure the Shell Launcher XML file, see [Create a Shell Launcher configuration file](configuration-file.md).

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg"::: **Intune/CSP**](#tab/intune)

You can configure devices using a [custom policy][MEM-1] with the [AssignedAccess CSP][WIN-3].

- **Setting:** `./Vendor/MSFT/AssignedAccess/ShellLauncher`
- **Value:** content of the XML configuration file

Assign the policy to a group that contains as members the devices that you want to configure.

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

[!INCLUDE [provisioning-package-1](../../../includes/configure/provisioning-package-1.md)]

- **Path:** `SMISettings/ShellLauncher`
- **Value:** depends on specific settings

[!INCLUDE [provisioning-package-2](../../../includes/configure/provisioning-package-2.md)]

#### [:::image type="icon" source="../images/icons/powershell.svg"::: **PowerShell**](#tab/ps)

[!INCLUDE [powershell-wmi-bridge-1](../../../includes/configure/powershell-wmi-bridge-1.md)]

```PowerShell
$shellLauncherConfiguration = @"

# content of the XML configuration file

"@

$namespaceName="root\cimv2\mdm\dmmap"
$className="MDM_AssignedAccess"
$obj = Get-CimInstance -Namespace $namespaceName -ClassName $className
$obj.ShellLauncher = [System.Net.WebUtility]::HtmlEncode($shellLauncherConfiguration)
$obj = Set-CimInstance -CimInstance $obj -ErrorVariable cimSetError -ErrorAction SilentlyContinue
if($cimSetError) {
    Write-Output "An ERROR occurred. Displaying error record and attempting to retrieve error logs...`n"
    Write-Error -ErrorRecord $cimSetError[0]

    $timeout = New-TimeSpan -Seconds 30
    $stopwatch = [System.Diagnostics.Stopwatch]::StartNew()
    $eventLogFilterHashTable = @{ LogName='Microsoft-Windows-AssignedAccess/Admin' }
    do{
        $events = Get-WinEvent -FilterHashtable $eventLogFilterHashTable -ErrorAction Ignore
    } until ($events.Count -or $stopwatch.Elapsed -gt $timeout) # wait for the log to be available

    if($events.Count) {
        $events | ForEach-Object {
            Write-Output "$($_.TimeCreated) [$($_.LevelDisplayName.ToUpper())] $($_.Message -replace "`n|`r")"
        }
    } else {
        Write-Warning "Timed-out attempting to retrieve event logs..."
    }

    Exit 1
}

Write-Output "Successfully applied Shell Launcher configuration"
```

[!INCLUDE [powershell-wmi-bridge-2](../../../includes/configure/powershell-wmi-bridge-2.md)]

---

> [!TIP]
> For practical examples, see the [Quickstart: configure a kiosk experience with Shell Launcher](quickstart-kiosk.md).

## User experience

After the settings are applied, the users that are configured to use Shell Launcher will execute the custom shell after sign-in.

Depending on your configuration, you can have a user to automatically sign in to the device.

## Remove Shell Launcher

Once you no longer need the kiosk configuration, you can remove it.

Here's a PowerShell example to remove the Shell Launcher configuration:

```powershell
$namespaceName="root\cimv2\mdm\dmmap"
$className="MDM_AssignedAccess"
$obj = Get-CimInstance -Namespace $namespaceName -ClassName $className
$obj.ShellLauncher = $null
Set-CimInstance -CimInstance $obj
```

## Next steps

> [!div class="nextstepaction"]
> Learn how to configure the Shell Launcher XML file:
>
> [Create a Shell Launcher configuration file](configuration-file.md)

<!--links-->

[MEM-1]: /mem/intune/configuration/custom-settings-windows-10
[WIN-3]: /windows/client-management/mdm/assignedaccess-csp
