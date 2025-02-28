---
title: Enable Shell Launcher
description: Learn how to enable the Shell Launcher feature.
ms.date: 02/27/2025
ms.topic: how-to
---

# Enable Shell Launcher

> [!NOTE]
> Configuring Shell Launcher using Assigned Access CSP, automatically enables Shell Launcher on the device, if the device supports it. There's no need to enable Shell Launcher separately if you configure it using Assigned Access CSP.

Shell Launcher is an optional component and isn't turned on by default in Windows. It must be turned on prior to configuring. You can turn on and configure Shell Launcher in a customized Windows 10 image (.wim) if Microsoft Windows hasn't been installed. If Windows has already been installed, you must turn on Shell Launcher before applying a provisioning package to configure Shell Launcher.

## Enable Shell Launcher using Control Panel

1. In the **Search the web and Windows** field, type **Programs and Features** and either press **Enter** or tap or select **Programs and Features** to open it.
1. In the **Programs and Features** window, select **Turn Windows features on or off**.
1. In the **Windows Features** window, expand the **Device Lockdown** node, select or clear the checkbox for **Shell Launcher**, and then select **OK.**
1. The **Windows Features** window indicates that Windows is searching for required files and displays a progress bar. Once found, the window indicates that Windows is applying the changes. When completed, the window indicates the requested changes are completed.
1. Select **Close** to close the **Windows Features** window.

> [!NOTE]
> Turning on Shell Launcher does not require a device restart.

## Enable Shell Launcher by calling WESL_UserSetting

1. Enable or disable Shell Launcher by calling the WESL_UserSetting. SetEnabled function in the Windows Management Instrumentation (WMI) class WESL_UserSetting
1. If you enable or disable Shell Launcher using WESL_UserSetting, the changes don't affect any sessions that are currently signed in; you must sign out and sign back in

This example uses a Windows image called install.wim, but you can use the same procedure to apply a provisioning package. For more information on DISM, see [What Is Deployment Image Servicing and Management](/windows-hardware/manufacture/desktop/what-is-dism).

## Enable Shell Launcher using DISM

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

## Enable Shell Launcher using Windows Configuration Designer

The Shell Launcher settings are also available as Windows provisioning settings so you can configure these settings to be applied during the image runtime. You can set one or all Shell Launcher settings by creating a provisioning package using Windows Configuration Designer and then applying the provisioning package during image deployment time or runtime. If Windows hasn't been installed and you're using Windows Configuration Designer to create installation media with settings for Shell Launcher included in the image or you're applying a provisioning package during setup, you must enable Shell Launcher on the installation media with DISM in order for a provisioning package to successfully apply.

Use the following steps to create a provisioning package that contains the ShellLauncher settings.

1. Build a provisioning package in Windows Configuration Designer by following the instructions in [Create a provisioning package for Windows](/windows/configuration/provisioning-packages/provisioning-create-package)
1. In the **Available customizations** page, select **Runtime settings** > **SMISettings** > **ShellLauncher**
1. Set the value of **Enable** to **ENABLE**. More options to configure Shell Launcher appears, and you can set the values as desired
1. Once you have finished configuring the settings and creating the provisioning package, you can apply the package to the image deployment time or runtime. See the [Apply a provisioning package](/windows/configuration/provisioning-packages/provisioning-apply-package) for more information. The process for applying the package to a Windows 10 Enterprise image is the same

## Next steps

> [!div class="nextstepaction"]
> Learn how to configure Shell Launcher:
>
> [Configure a kiosk with Shell Launcher](configure.md)
