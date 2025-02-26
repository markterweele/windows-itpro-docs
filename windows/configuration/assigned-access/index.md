---
title: What is Assigned Access?
description: Learn how to configure a Windows kiosk for single-app and multi-app scenarios with Assigned Access.
ms.date: 10/31/2024
ms.topic: overview
---

# What is Assigned Access?

Assigned Access is a Windows feature that you can use to configure a device as a kiosk or with a restricted user experience.

When you configure a **kiosk experience**, a single Universal Windows Platform (UWP) application or Microsoft Edge is executed in full screen, above the lock screen. Users can only use that application. If the kiosk app is closed, it automatically restarts. Practical examples include:

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
