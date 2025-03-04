---
title: Configure the Settings Page Visibility in Windows
description: Learn how to configure the pages listed in the Windows Settings app.
ms.topic: how-to
ms.date: 03/03/2025
author: paolomatarazzo
ms.author: paoloma
---

# Configure the Settings Page Visibility in Windows

*Settings* is a Windows application that provides users with a unified interface to manage their system settings. However, in certain scenarios, you may want to restrict access to specific settings pages to ensure a more controlled and secure environment. This is especially beneficial for devices used in specific environments, such as kiosks or student devices, where limiting access to certain settings can prevent unauthorized changes and maintain a consistent user experience.

:::image type="content" source="images/settings-page-visibility.png" alt-text="Screenshot of the Settings app configured with a policy setting to limit the categories displayed.":::

You can configure the visibility of settings pages using the *page visibility list* policy setting. This policy allows you to block a given set of pages from the Settings app. Blocked pages won't be visible in the app, and if all pages in a category are blocked, the category is hidden too. Direct navigation to a blocked page via URI, context menu in Explorer or other means results in the first page of Settings displayed instead.

This policy has two modes:

- Specify a list of settings pages to show. In this case, the policy string must begin with `showonly:`. After this, the policy string must contain a semicolon-delimited list of settings page identifiers. The identifier for any given settings page is the published URI for that page, minus the `ms-settings: protocol part
- Specify a list of pages to hide. In this case, the policy string must begin with `hide:`. After this, the policy string must contain a semicolon-delimited list of settings page identifiers. The identifier for any given settings page is the published URI for that page, minus the `ms-settings:` protocol part

## Examples

> [!NOTE]
> The availability of per-user support is documented [here](https://go.microsoft.com/fwlink/?linkid=2102995).

To specify that only the **About** and **Bluetooth** pages should be shown (their respective URIs are `ms-settings:about` and `ms-settings:bluetooth`) and all other pages hidden:

`showonly:about;bluetooth`

To specify that only the Bluetooth page (URI `ms-settings:bluetooth`) should be hidden:

`hide:bluetooth`

## Configuration

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg" border="false"::: **Intune/CSP**](#tab/intune)

[!INCLUDE [intune-settings-catalog-1](../../../includes/configure/intune-settings-catalog-1.md)]

| Category | Setting name | Value |
|--|--|--|
| **Settings** | - Page Visibility List<br>- Page Visibility List (User)| List of URIs to show or hide, separated by semicolons.|

[!INCLUDE [intune-settings-catalog-2](../../../includes/configure/intune-settings-catalog-2.md)]

Alternatively, you can configure devices using a [custom policy][INT-1] with the [Policy CSP](/windows/client-management/mdm/policy-csp-settings#pagevisibilitylist).

| Setting |
|--|
|- **OMA-URI:** `./Device/Vendor/MSFT/Policy/Config/Settings/PageVisibilityList`<br>- **Data type:** string<br>- **Value:** List of URIs to show or hide, separated by semicolons.|
|- **OMA-URI:** `./User/Vendor/MSFT/Policy/Config/Settings/PageVisibilityList`<br>- **Data type:** string<br>- **Value:** List of URIs to show or hide, separated by semicolons.|

#### [:::image type="icon" source="../images/icons/group-policy.svg" border="false"::: **GPO**](#tab/gpo)

[!INCLUDE [gpo-settings-1](../../../includes/configure/gpo-settings-1.md)]

| Group policy path | Group policy setting | Value |
| - | - | - |
| **Computer Configuration** > **Administrative Templates** > **Control Panel** > **Settings Page Visibility** | Turn off the Store application| **Enabled**|
| **User Configuration** > **Administrative Templates** > **Control Panel** > **Settings Page Visibility** | Turn off the Store application| **Enabled**|

[!INCLUDE [gpo-settings-2](../../../includes/configure/gpo-settings-2.md)]

---

## User Experience

By controlling the visibility of Settings pages, you can create a customized user experience tailored to your organization's specific needs. Once the policy is applied, users will have access only to the Settings pages you have explicitly allowed, ensuring a focused and streamlined interface.
