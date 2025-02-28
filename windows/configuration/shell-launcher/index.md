---
title: Shell Launcher Overview
description: Learn how to configure devices with Shell Launcher.
ms.date: 02/27/2025
ms.topic: overview
---

# Shell Launcher overview

Shell Launcher is a Windows feature that you can use to replace the default Windows Explorer shell (`Explorer.exe`) with a Windows desktop application or a Universal Windows Platform (UWP) app. This feature is useful for creating a custom user experience on devices that are used for a specific purpose, including kiosks, ATMs, and digital signage.

Shell Launcher controls which application a user gets as the shell after sign-in. It doesn't prevent a user from accessing other desktop applications and system components. From a custom shell, you can launch secondary views displayed on multiple monitors, or launch other apps in full screen on user's demand. You can also configure Shell Launcher to launch different shell applications for different users or user groups.

With Shell Launcher, you can use features and methods to control access to other applications or system components. These methods include, but aren't limited to:

- Configuration Service Provider (CSP): you can use a Mobile Device Management (MDM) solution like Microsoft Intune
- Group policy (GPO)
- [AppLocker](/windows/security/threat-protection/windows-defender-application-control/applocker/applocker-overview)

> [!NOTE]
>Shell Launcher is part of the Assigned Access feature, which allows you to configure kiosks or restricted user experiences. To learn about the differences between Shell Launcher and the other options offered by Assigned Access, see [Windows Kiosks Configuration Options Overview](../kiosk/index.md).

[!INCLUDE [shell-launcher](../../../includes/licensing/shell-launcher.md)]

## Shell Launcher user rights

A custom shell is launched with the same level of user rights as the account that is signed in. This means that a user with administrative rights can perform any system action that requires administrative rights, including launching other applications with administrative rights.

> [!WARNING]
> If your shell application requires administrative rights and needs to be elevated, and User Account Control (UAC) is enabled, you must disable UAC for Shell Launcher to launch the shell application.

## Limitations

Here are some limitations to consider when using Shell Launcher:

- Windows doesn't support setting a custom shell before the out-of-box experience (OOBE). If you do, you can't deploy the resulting image
- Shell Launcher doesn't support a custom shell with an application that launches a different process and exits. For example, you can't specify `write.exe` in Shell Launcher. Shell Launcher launches a custom shell and monitors the process to identify when the custom shell exits. `Write.exe` creates a 32-bit `wordpad.exe` process and exits. Since Shell Launcher isn't aware of the newly created `wordpad.exe` process, Shell Launcher takes action based on the exit code of `Write.exe`, such as restarting the custom shell

## Next steps

Learn how to configure Shell Launcher:

- [Configure a kiosk with Shell Launcher](configure.md)

### :::image type="icon" source="../images/icons/rocket.svg" border="false"::: Quickstarts

If you want to quickly test Shell Launcher, check out the following quickstart:

- [Quickstart: configure a kiosk with Shell Launcher](quickstart-kiosk.md)