---
title: Shell Launcher
description: Shell Launcher
ms.date: 06/07/2018
ms.topic: overview
---

# Shell Launcher exceptions

There are a few exceptions to the applications and executables you can use as a custom shell:

- You can't use the following executable as a custom shell: `C:\Windows\System32\Eshell.exe`. Using Eshell.exe as the default shell will result in a blank screen after user signs in.
- You can't use a Universal Windows app as a custom shell.
- You can't use a custom shell to launch Universal Windows apps, for example, the Settings app.
- You can't use an application that launches a different process and exits as a custom shell. For example, you can't specify **write.exe** in Shell Launcher. Shell Launcher launches a custom shell and monitors the process to identify when the custom shell exits. **Write.exe** creates a 32-bit wordpad.exe process and exits. Because Shell Launcher isn't aware of the newly created wordpad.exe process, Shell Launcher takes action based on the exit code of **Write.exe**, and restart the custom shell.
- You can't prevent the system from shutting down. For Shell Launcher V1 and V2, you can't block the session ending by returning FALSE upon receiving the [WM_QUERYENDSESSION](/windows/win32/shutdown/wm-queryendsession) message in a graphical application or returning FALSE in the [handler routine](/windows/console/handlerroutine) that is added through the [SetConsoleCtrlHandler](/windows/console/setconsolectrlhandler) function in a console application.

> [!NOTE]
> You cannot configure both Shell Launcher and assigned access on the same system.

Shell Launcher processes the **Run** and **RunOnce** registry keys before starting the custom shell, so your custom shell doesn't need to handle the automatic startup of other applications and services.

Shell Launcher also handles the behavior of the system when your custom shell exits. You can configure the shell exit behavior if the default behavior doesn't meet your needs.

Methods of controlling access to other desktop applications and system components can be used in addition to using the Shell Launcher such as, [Group Policy](https://www.microsoft.com/download/details.aspx?id=25250), [AppLocker](/windows/iot/iot-enterprise/customize/application-control#applocker), and [Mobile Device Management](/windows/client-management/mdm/)

## Differences between Shell Launcher v1 and Shell Launcher v2

- Shell Launcher v1 replaces `explorer.exe`, the default shell, with `eshell.exe`, which can launch a Windows desktop application
- Shell Launcher v2 replaces `explorer.exe` with `customshellhost.exe`, which can launch a Windows desktop application or a UWP app
- In addition to allowing you to use a UWP app for your replacement shell, Shell Launcher v2 offers more enhancements:
  - You can use a custom Windows desktop application that can then launch UWP apps, such as Settings and Touch Keyboard.
  - From a custom UWP shell, you can launch secondary views and run on multiple monitors.
  - The custom shell app runs in full screen, and can run other apps in full screen on user's demand.

For sample XML configurations for the different app combinations, see [Samples for Shell Launcher v2](https://github.com/microsoft/Windows-IoT-Samples/tree/master/samples/ShellLauncher/ShellLauncherV2).



## FROM COPILOT

Shell Launcher is a feature in Windows that allows administrators to replace the default Windows Explorer shell with a custom shell for specialized devices or environments. Over time, Shell Launcher has evolved to meet the needs of modern deployments, leading to the introduction of Shell Launcher v2.

Shell Launcher v1 was the original implementation, introduced to provide basic functionality for replacing the default shell. However, it had limitations, such as only supporting Win32 applications as custom shells and lacking flexibility for handling modern app scenarios.

Shell Launcher v2, introduced with Windows 10, version 1809, brought significant enhancements. It added support for Universal Windows Platform (UWP) apps as custom shells, making it more versatile for modern environments. Additionally, v2 introduced the ability to configure fallback shells, ensuring a more robust experience in case the primary shell fails to launch. This feature is particularly useful for maintaining system reliability in critical-use cases, such as kiosks or embedded systems.

Shell Launcher v2 is the preferred choice because it:

Supports both Win32 and UWP apps, offering greater flexibility.
Provides fallback shell functionality, improving system resilience.
Is better suited for modern Windows environments, especially those leveraging UWP apps or mixed app ecosystems.
By upgrading to Shell Launcher v2, administrators can take advantage of these improvements to create more reliable and adaptable custom shell experiences.