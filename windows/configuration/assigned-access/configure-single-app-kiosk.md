---
title: Configure a Single-App Kiosk With Assigned Access
description: Learn how to configure a single-app kiosk with Assigned Access.
ms.date: 3/7/2025
ms.topic: overview
---

# Configure a single-app kiosk with Assigned Access

Assigned Access is a Windows feature that you can use to configure a device as a kiosk or with a restricted user experience.

When you configure a **kiosk experience**, a single Universal Windows Platform (UWP) application or Microsoft Edge is executed in full screen. Users can only use that application and once the kiosk app is closed, it automatically restarts. Practical examples include:

- Public browsing
- Interactive digital signage

When you configure a **restricted user experience**, users can only execute a defined list of applications, with a tailored Start menu and Taskbar. Different policy settings and AppLocker rules are enforced, creating a locked down experience. The users can access a familiar Windows desktop, while limiting their access, reducing distractions, and potential for inadvertent uses. Ideal for shared devices, you can create different configurations for different users. Practical examples include:

- Frontline worker devices
- Student devices
- Lab devices

> [!NOTE]
> When you configure a restricted user experience, different policy settings are applied to the device. Some policy settings apply to standard users only, and some to administrator accounts too. For more information, see [Assigned Access policy settings](policy-settings.md).

## Requirements

Here are the requirements for Assigned Access:

- To use a kiosk experience, [User account control (UAC)](/windows/security/identity-protection/user-account-control/user-account-control-overview) must be enabled
- To use a kiosk experience, you must sign in from the console. The kiosk experience isn't supported over a remote desktop connection

[!INCLUDE [assigned-access](../../../includes/licensing/assigned-access.md)]

## Configure a kiosk experience

There are several options to configure a kiosk experience. If you need to configure a single device with a local account, you can use:

- PowerShell: you can use the `Set-AssignedAccess` PowerShell cmdlet to configure a kiosk experience using a local standard account
- Settings: use this option when you need a simple method to configure a single device with a local standard user account

For advanced customizations, you can use the [Assigned Access CSP](/windows/client-management/mdm/assignedaccess-csp) to configure the kiosk experience. The CSP allows you to configure the kiosk app, the user account, and the kiosk app's behavior. When you use the CSP, you must create an XML configuration file that specifies the kiosk app and the user account. The XML file is applied to the device using one of the following options:

- A Mobile Device Management (MDM) solution, like Microsoft Intune
- Provisioning packages
- PowerShell, with the MDM Bridge WMI Provider

To learn how to configure the Shell Launcher XML file, see [Create an Assigned Access configuration file](configuration-file.md).

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg"::: **Intune/CSP**](#tab/intune)

You can configure devices using a [custom policy][MEM-1] with the [AssignedAccess CSP][WIN-3].

- **Setting:** `./Vendor/MSFT/AssignedAccess/Configuration`
- **Value:** content of the XML configuration file

Assign the policy to a group that contains as members the devices that you want to configure.

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

[!INCLUDE [provisioning-package-1](../../../includes/configure/provisioning-package-1.md)]

- **Path:** `AssignedAccess/AssignedAccessSettings`
- **Value:** Enter the account and the application you want to use for Assigned access, using the AUMID of the app. Example:
  - `{"Account":"domain\user", "AUMID":"Microsoft.WindowsCalculator_8wekyb3d8bbwe!App"}`

[!INCLUDE [provisioning-package-2](../../../includes/configure/provisioning-package-2.md)]

#### [:::image type="icon" source="../images/icons/powershell.svg"::: **PowerShell**](#tab/ps)

To configure a device using Windows PowerShell:

1. Sign in as administrator
1. [Create the user account](https://support.microsoft.com/help/4026923/windows-create-a-local-user-or-administrator-account-in-windows-10) for Assigned Access
1. Sign in as the Assigned Access user account
1. Install the required UWP app
1. Sign out as the Assigned Access user account
1. Sign in as administrator and from an elevated PowerShell prompt use one of the following commands:

    ```PowerShell
    #Configure Assigned Access by AppUserModelID and user name
    Set-AssignedAccess -AppUserModelId <AUMID> -UserName <username>

    #Configure Assigned Access by AppUserModelID and user SID
    Set-AssignedAccess -AppUserModelId <AUMID> -UserSID <usersid>

    #Configure Assigned Access by app name and user name
    Set-AssignedAccess -AppName <CustomApp> -UserName <username>

    #Configure Assigned Access by app name and user SID**:
    Set-AssignedAccess -AppName <CustomApp> -UserSID <usersid>

> [!NOTE]
> To set up Assigned Access using `-AppName`, the user account that you enter for Assigned Access must have signed in at least once.

For more information:

- [Find the Application User Model ID of an installed app](../store/find-aumid.md)
- [Set-AssignedAccess](/powershell/module/assignedaccess/set-assignedaccess)

To remove assigned access, using PowerShell, run the following cmdlet:

```powershell
Clear-AssignedAccess
```

For advanced customizations that use the XML configuration file, you can use PowerShell scripts via the [MDM Bridge WMI Provider](/windows/win32/dmwmibridgeprov/mdm-bridge-wmi-provider-portal).

> [!IMPORTANT]
> For all device settings, the WMI Bridge client must be executed as SYSTEM (LocalSystem) account.

To test the PowerShell script, you can:

1. [Download the psexec tool](/sysinternals/downloads/psexec)
1. Open an elevated command prompt and run: `psexec.exe -i -s powershell.exe`
1. Run the script in the PowerShell session

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

#### [:::image type="icon" source="../images/icons/settings-app.svg"::: **Settings**](#tab/settings)

Here are the steps to configure a kiosk using the Settings app:

1. Open the Settings app to view and configure a device as a kiosk. Go to **Settings > Accounts > Other Users**, or use the following shortcut:

    > [!div class="nextstepaction"]
    >
    > [Other Users](ms-settings:otherusers)

1. Under **Set up a kiosk**, select **Get Started**
1. In the **Create an account** dialog, enter the account name, and select **Next**
    >[!NOTE]
    >If there are any local standard user accounts already, the **Create an account** dialog offers the option to **Choose an existing account**

1. Choose the application to run when the kiosk account signs in. If you select **Microsoft Edge** as the kiosk app, you configure the following options:

    - Whether Microsoft Edge should display your website full-screen (digital sign) or with some browser controls available (public browser)
    - Which URL should be open when the kiosk accounts signs in
    - When Microsoft Edge should restart after a period of inactivity (if you select to run as a public browser)

1. Select **Close**

When the device isn't joined to an Active Directory domain or Microsoft Entra ID, automatic sign-in of the kiosk account is configured automatically:

- If you want the kiosk account to sign in automatically, and the kiosk app launched when the device restarts, then you don't need to do anything
- If you don't want the kiosk account to sign in automatically when the device restarts, then you must change the default setting before you configure the device as a kiosk. Sign in with the account that you want to use as the kiosk account. Open **Settings** > **Accounts** > **Sign-in options**. Set the **Use my sign-in info to automatically finish setting up my device after an update or restart** setting to **Off**. After you change the setting, you can apply the kiosk configuration to the device

---

> [!TIP]
> For practical examples, see the [Quickstart: Configure a kiosk with Assigned Access](quickstart-kiosk.md).

[!INCLUDE [user-experience](includes/user-experience.md)]

[MEM-1]: /mem/intune/configuration/custom-settings-windows-10
[WIN-3]: /windows/client-management/mdm/assignedaccess-csp
