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
1. Select **OK** to enable Shell Launcher

#### [:::image type="icon" source="../images/icons/powershell.svg"::: **PowerShell**](#tab/powershell)

To enable Shell Launcher using PowerShell, follow these steps:

1. Open a PowerShell window with administrator privileges
1. Run the following command:

    ```powershell
    Enable-WindowsOptionalFeature -FeatureName Client-DeviceLockdown,Client-EmbeddedShellLauncher -Online
    ```

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

[!INCLUDE [provisioning-package-1](../../../includes/configure/provisioning-package-1.md)]

- **Path:** `SMISettings/ShellLauncher/Enable`
- **Value:**  ENABLE

[!INCLUDE [provisioning-package-2](../../../includes/configure/provisioning-package-2.md)]

> [!IMPORTANT]
> You can configure Shell Launcher by creating a provisioning package and then applying the provisioning package during image deployment time or at runtime. If you're creating an installation media with settings for Shell Launcher included in the image, or you're applying a provisioning package during setup, you must enable Shell Launcher on the installation media with DISM for a provisioning package to successfully apply.

#### [:::image type="icon" source="../images/icons/settings.svg"::: **DISM**](#tab/dism)

The following example uses a Windows image called `install.wim`, but you can use the same procedure to apply a provisioning package.

1. Open a command prompt with administrator privileges.
1. Copy install.wim to a temporary folder on hard drive (in the following steps, we assume it's called `C:\wim`)
1. Modify the following script to match your environment:

```cmd
@echo off
REM Create a new directory
md c:\wim

REM Mount the image
dism /mount-wim /wimfile:c:\bootmedia\sources\install.wim /index:1 /MountDir:c:\wim

REM Enable the feature
dism /image:c:\wim /enable-feature /all /featureName:Client-EmbeddedShellLauncher

REM Commit the change
dism /unmount-wim /MountDir:c:\wim /Commit
```

For more information on DISM, see [What Is Deployment Image Servicing and Management](/windows-hardware/manufacture/desktop/what-is-dism).

#### [:::image type="icon" source="../images/icons/dev.svg"::: **WMI**](#tab/wmi)

You can enable or disable Shell Launcher by calling the `SetEnabled` function in the Windows Management Instrumentation (WMI) class `WESL_UserSetting`.

For more information, see [WESL_UserSetting](wesl-usersetting.md).

---
