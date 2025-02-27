---
title: Shell Launcher Overview
description: Learn how to configure devices with Shell Launcher.
ms.date: 02/27/2025
ms.topic: overview
---

# Shell Launcher Overview

Shell Launcher is a Windows feature that you can use to replace the default Windows Explorer shell (`Explorer.exe`) with a Windows desktop application or a Universal Windows Platform (UWP) app.

Practical examples include:

- Public browsing
- Interactive digital signage
- ATMs

Shell Launcher controls which application the user sees as the shell after sign-in. It doesn't prevent the user from accessing other desktop applications and system components. From a custom shell, you can launch secondary views displayed on multiple monitors, or launch other apps in full screen on user's demand.

With Shell Launcher, you can use features and methods to control access to other applications or system components. These methods include, but aren't limited to:

- Configuration Service Provider (CSP): you can use a Mobile Device Management (MDM) solution like Microsoft Intune
- Group policy (GPO)
- [AppLocker](/windows/security/threat-protection/windows-defender-application-control/applocker/applocker-overview)

Shell Launcher is part of the Assigned Access feature, which allows you to configure kiosks or restricted user experiences. To learn about the differences between Shell Launcher and the other options offered by Assigned Access, see [Windows kiosks and restricted user experiences](../kiosk/index.md).

[!INCLUDE [shell-launcher](../../../includes/licensing/shell-launcher.md)]

## Limitations

Here are some limitations to consider when using Shell Launcher:

- Windows doesn't support setting a custom shell before the out-of-box experience (OOBE). If you do, you can't deploy the resulting image
- Shell Launcher doesn't support a custom shell with an application that launches a different process and exits. For example, you can't specify `write.exe` in Shell Launcher. Shell Launcher launches a custom shell and monitors the process to identify when the custom shell exits. `Write.exe` creates a 32-bit `wordpad.exe` process and exits. Since Shell Launcher isn't aware of the newly created `wordpad.exe` process, Shell Launcher takes action based on the exit code of `Write.exe`, such as restarting the custom shell
