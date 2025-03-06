---
title: Enable Shell Launcher
description: Learn how to enable the Shell Launcher feature.
ms.date: 02/27/2025
ms.topic: how-to
---

# Enable Shell Launcher

Shell Launcher is an optional component in Windows that is not enabled by default. To configure it, you must first enable it. You can enable and configure Shell Launcher in a customized Windows image, or you can enable it before applying a provisioning package to configure it.

> [!NOTE]
> When you configure Shell Launcher with the Assigned Access Configuration Service Provider (CSP), Shell Launcher is automatically enabled, if the device supports it. There's no need to enable Shell Launcher separately when you configure it using Assigned Access CSP.

There are multiple ways to enable Shell Launcher, select the method that best fits your needs to learn more.

#### [:::image type="icon" source="../images/icons/control-panel.svg"::: **Control Panel**](#tab/control-panel)

To enable Shell Launcher using Control Panel, follow these steps:

1. Open **Control Panel** > **Programs** > **Turn Windows features on or off** or use the command `optionalfeatures.exe`
1. Expand **Device Lockdown** and select **Shell Launcher**

#### [:::image type="icon" source="../images/icons/powershell.svg"::: **PowerShell**](#tab/powershell)

To enable Shell Launcher using PowerShell, follow these steps:

1. Open a PowerShell window with administrator privileges
1. Run the following command to enable Shell Launcher:

    ```powershell
    Enable-WindowsOptionalFeature -FeatureName Client-DeviceLockdown,Client-EmbeddedShellLauncher -Online
    ```

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

The Shell Launcher settings are also available as Windows provisioning settings so you can configure these settings to be applied during the image runtime. You can set one or all Shell Launcher settings by creating a provisioning package using Windows Configuration Designer and then applying the provisioning package during image deployment time or runtime. If Windows hasn't been installed and you're using Windows Configuration Designer to create installation media with settings for Shell Launcher included in the image or you're applying a provisioning package during setup, you must enable Shell Launcher on the installation media with DISM in order for a provisioning package to successfully apply.

Use the following steps to create a provisioning package that contains the ShellLauncher settings.

1. Build a provisioning package in Windows Configuration Designer by following the instructions in [Create a provisioning package for Windows](/windows/configuration/provisioning-packages/provisioning-create-package)
1. In the **Available customizations** page, select **Runtime settings** > **SMISettings** > **ShellLauncher**
1. Set the value of **Enable** to **ENABLE**. More options to configure Shell Launcher appears, and you can set the values as desired
1. Once you have finished configuring the settings and creating the provisioning package, you can apply the package to the image deployment time or runtime. See the [Apply a provisioning package](/windows/configuration/provisioning-packages/provisioning-apply-package) for more information. The process for applying the package to a Windows 10 Enterprise image is the same


| Path | Setting name | Value |
|--|--|--|
| `Policies/Authentication` | `EnableWebSignIn` | Enabled |
| `Policies/Authentication` | `ConfigureWebSignInAllowedUrls` | This setting is optional, and it contains a semicolon-separated list of domains required for sign in, for example: `idp.example.com;example.com` |
| `Policies/Authentication` | `ConfigureWebCamAccessDomainNames` | This setting is optional, and it should be configured if you need to use the webcam during the sign-in process. Specify the list of domains that are allowed to use the webcam during the sign-in process, separated by a semicolon. For example: `example.com` |

#### [:::image type="icon" source="../images/icons/settings.svg"::: **DISM**](#tab/dism)

1. Open a command prompt with administrator privileges.
1. Copy install.wim to a temporary folder on hard drive (in the following steps, we assume it's called `C:\wim`)
1. Create a new directory

    ```CMD
    md c:\wim
    ```

1. Mount the image

    ```CMD
    dism /mount-wim /wimfile:c:\bootmedia\sources\install.wim /index:1 /MountDir:c:\wim
    ```

1. Enable the feature

    ```CMD
    dism /image:c:\wim /enable-feature /all /featureName:Client-EmbeddedShellLauncher
    ```

1. Commit the change

    ```CMD
    dism /unmount-wim /MountDir:c:\wim /Commit
    ```

#### [:::image type="icon" source="../images/icons/dev.svg"::: **WMI**](#tab/wmi)

Enable Shell Launcher by calling WESL_UserSetting

1. Enable or disable Shell Launcher by calling the WESL_UserSetting. SetEnabled function in the Windows Management Instrumentation (WMI) class WESL_UserSetting
1. If you enable or disable Shell Launcher using WESL_UserSetting, the changes don't affect any sessions that are currently signed in; you must sign out and sign back in

This example uses a Windows image called install.wim, but you can use the same procedure to apply a provisioning package. For more information on DISM, see [What Is Deployment Image Servicing and Management](/windows-hardware/manufacture/desktop/what-is-dism).


---
