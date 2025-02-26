---
title: Configure a multi-app kiosk with Assigned Access
description: Learn how to configure a multi-app kiosk with Assigned Access.
ms.date: 10/31/2024
ms.topic: overview
---

# Configure a restricted user experience (multi-app kiosk) with Assigned Access

To configure a restricted user experience with Assigned Access, you must create an XML configuration file with the settings for the desired experience. The XML file is applied to the device via the [Assigned Access CSP](/windows/client-management/mdm/assignedaccess-csp#shelllauncher), using one of the following options:

- A Mobile Device Management (MDM) solution, like Microsoft Intune
- Provisioning packages
- PowerShell, with the MDM Bridge WMI Provider

To learn how to configure the Assigned Access XML file, see [Create an Assigned Access configuration file](configuration-file.md).

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg"::: **Intune/CSP**](#tab/intune)

You can configure devices using a [custom policy][MEM-1] with the [AssignedAccess CSP][WIN-3].

- **Setting:** `./Vendor/MSFT/AssignedAccess/ShellLauncher`
- **Value:** content of the XML configuration file

Assign the policy to a group that contains as members the devices that you want to configure.

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

[!INCLUDE [provisioning-package-1](../../../includes/configure/provisioning-package-1.md)]

- **Path:** `AssignedAccess/MultiAppAssignedAccessSettings`
- **Value:**  content of the XML configuration file

[!INCLUDE [provisioning-package-2](../../../includes/configure/provisioning-package-2.md)]

#### [:::image type="icon" source="../images/icons/powershell.svg"::: **PowerShell**](#tab/ps)

[!INCLUDE [powershell-wmi-bridge-1](../../../includes/configure/powershell-wmi-bridge-1.md)]

```PowerShell
$assignedAccessConfiguration = @"

# content of the XML configuration file

"@

$namespaceName="root\cimv2\mdm\dmmap"
$className="MDM_AssignedAccess"
$obj = Get-CimInstance -Namespace $namespaceName -ClassName $className
$obj.Configuration = [System.Net.WebUtility]::HtmlEncode($assignedAccessConfiguration)
$obj = Set-CimInstance -CimInstance $obj -ErrorVariable cimSetError -ErrorAction SilentlyContinue
if($cimSetError) {
    Write-Output "An ERROR occurred. Displaying error record and attempting to retrieve error logs...`n"
    Write-Error -ErrorRecord $cimSetError[0]

    $timeout = New-TimeSpan -Seconds 30
    $stopwatch = [System.Diagnostics.Stopwatch]::StartNew()
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

Write-Output "Successfully applied Assigned Access configuration"
```

[!INCLUDE [powershell-wmi-bridge-2](../../../includes/configure/powershell-wmi-bridge-2.md)]

#### [:::image type="icon" source="../images/icons/settings-app.svg"::: **Settings**](#tab/settings)

This option isn't available using Settings.

---

> [!TIP]
> For practical examples, see the [Quickstart: Configure a restricted user experience with Assigned Access](quickstart-restricted-user-experience.md)

## User experience

To validate the kiosk or restricted user experience, sign in with the user account you specified in the configuration file.

The Assigned Access configuration takes effect the next time the targeted user signs in. If that user account is signed in when you apply the configuration, sign out and sign back in to validate the experience.

> [!NOTE]
> Starting in Windows 11, a restricted user experience supports the use of multiple monitors.

### Autotrigger touch keyboard

The touch keyboard is automatically triggered when there's an input needed and no physical keyboard is attached on touch-enabled devices. You don't need to configure any other setting to enforce this behavior.

> [!TIP]
> The touch keyboard is triggered only when tapping a textbox. Mouse clicks don't trigger the touch keyboard. If you're testing this feature, use a physical device instead of a virtual machine (VM), as the touch keyboard is not triggered on VMs.

### Sign out of assigned access

By default, to exit the kiosk experience, press <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Del</kbd>. The kiosk app exits automatically. If you sign in again as the Assigned Access account, or wait for the sign in screen timeout, the kiosk app relaunches. The default timeout is 30 seconds, but you can change the timeout with the registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI`

To change the default time for Assigned Access to resume, add *IdleTimeOut* (DWORD) and enter the value data as milliseconds in hexadecimal.

> [!NOTE]
> `IdleTimeOut` doesn't apply to the Microsoft Edge kiosk mode.

The Breakout Sequence of <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Del</kbd> is the default, but this sequence can be configured to be a different sequence of keys. The breakout sequence uses the format **modifiers + keys**. An example breakout sequence is <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>A</kbd>, where <kbd>CTRL</kbd> + <kbd>ALT</kbd> are the modifiers, and <kbd>A</kbd> is the key value. To learn more, see [Create an Assigned Access configuration XML file](configuration-file.md).

## Remove Assigned Access

Deleting the restricted user experience removes the policy settings associated with the users, but it can't revert all the configurations. For example, the Start menu configuration is maintained.

## Next steps

> [!div class="nextstepaction"]
> Review the recommendations before you deploy Assigned Access:
>
> [Assigned Access recommendations](recommendations.md)

<!--links-->

[MEM-1]: /mem/intune/configuration/custom-settings-windows-10
[WIN-3]: /windows/client-management/mdm/assignedaccess-csp
