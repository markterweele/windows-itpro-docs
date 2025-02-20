---
author: paolomatarazzo
ms.author: paoloma
ms.date: 04/10/2024
ms.topic: include
---

### Hide recently added apps

With this policy setting, you can prevent the Start menu from displaying a list of recently installed applications:

- If **enabled**, the Start menu doesn't display the **Recently added** list. The corresponding option in Settings can't be configured (grayed out).
- If **disabled** or **not configured**, the Start menu displays the **Recently added** list. The corresponding option in Settings can be configured.

> [!IMPORTANT]
> Starting in Windows 11, version 22H2 with [KB5048685](https://support.microsoft.com/topic/4602-ea3736d3-6948-4fd7-9faf-8d732ac2ed59), the policy setting behavior changed.
>
> - If **enabled**, the corresponding option in Settings can't be configured (grayed out). The policy setting doesn't affect the display of recently installed applications in the Recommended section of the Start menu.
> - If **disabled** or **not configured**, the corresponding option in Settings can be configured.

|  | Path |
|--|--|
| **CSP** | `./Device/Vendor/MSFT/Policy/Config/Start/`[HideRecentlyAddedApps](/windows/client-management/mdm/policy-csp-start#hiderecentlyaddedapps)<br><br>`./User/Vendor/MSFT/Policy/Config/Start/`[HideRecentlyAddedApps](/windows/client-management/mdm/policy-csp-start#hiderecentlyaddedapps) |
| **GPO** | **Computer Configuration** > **Administrative Templates** > **Start Menu and Taskbar**<br><br> **User Configuration** > **Administrative Templates** > **Start Menu and Taskbar** > **Remove "Recently added" list from Start Menu** |
