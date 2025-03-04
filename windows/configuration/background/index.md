---
title: Configure the Desktop and Lock Screen Background in Windows
description: Learn how to configure the desktop and lock screen background in Windows using policy settings, including Intune, CSP and GPO.
ms.topic: how-to
ms.date: 03/03/2025
author: paolomatarazzo
ms.author: paoloma
appliesto:
zone_pivot_groups: windows-versions-11-10
---

# Configure the desktop and lock screen background

Configuring desktop and lock screen backgrounds in Windows offers a simple yet effective way to enhance productivity, enforce consistency, and strengthen organizational branding. Predefined backgrounds can display company logos, mission statements, or school emblems, reinforcing identity across devices. This is especially valuable for kiosks, where lock screens can provide clear instructions, or student devices, where consistent branding fosters a sense of belonging and professionalism.

::: zone pivot="windows-11"

:::image type="content" source="images/contoso-lockscreen-11.png" alt-text="Screenshot of the Windows 11 lock screen with Windows spotlight enabled over an organization wallpaper." border="false":::

::: zone-end

::: zone pivot="windows-10"

:::image type="content" source="images/contoso-lockscreen-10.png" alt-text="Screenshot of the Windows 10 lock screen with Windows spotlight enabled over an organization wallpaper." border="false":::

::: zone-end

This article describes how to configure the desktop and lock screen background in Windows using policy settings. The article also provides examples of how to configure the settings using Microsoft Intune, the Configuration Service Provider (CSP), and Group Policy Object (GPO).

## Image ratios and scaling

A concern with custom images is how they'll appear on different screen sizes and resolutions. A custom image created in `16:9` aspect ratio (for example, `1600x900`) scales properly on devices using a `16:9` resolution, such as `1280x720` or `1920x1080`. On devices using other aspect ratios, such as `4:3` (`1024x768`) or `16:10` (`1280x800`), height scales correctly and width is cropped to a size equal to the aspect ratio. The image remains centered on the screen.

Images created at other aspect ratios might scale and center unpredictably on your device when changing aspect ratios. The recommendation for custom images that include text (such as a legal statement), is to create the image in `16:9` resolution with text contained in the `4:3` region, allowing the text to remain visible at any aspect ratio.

## Configure the desktop background

You can use configuration service provider (CSP) or group policy (GPO) settings to configure access to the Microsoft Store app. The CSP configuration is available to Windows Enterprise and Education editions only.

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg" border="false"::: **Intune/CSP**](#tab/intune)

To configure the desktop background, you can use:

- Microsoft Intune/MDM
- Group policy
- Registry

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg" border="false"::: **Intune/CSP**](#tab/intune)

[!INCLUDE [intune-settings-catalog-1](../../../includes/configure/intune-settings-catalog-1.md)]

| Category | Setting name | Value |
|--|--|--|
| **Administrative Templates > System > Credentials Delegation** | Remote host allows delegation of nonexportable credentials | Enabled |

[!INCLUDE [intune-settings-catalog-2](../../../includes/configure/intune-settings-catalog-2.md)]

Alternatively, you can configure devices using a [custom policy][INT-3] with the [Policy CSP][CSP-1].

| Setting |
|--------|
| - **OMA-URI:** `./Device/Vendor/MSFT/Policy/Config/CredentialsDelegation/RemoteHostAllowsDelegationOfNonExportableCredentials`<br>- **Data type:** string<br>- **Value:** `<enabled/>`|

#### [:::image type="icon" source="../images/icons/group-policy.svg" border="false"::: **GPO**](#tab/gpo)

[!INCLUDE [gpo-settings-1](../../../includes/configure/gpo-settings-1.md)]

| Group policy path | Group policy setting | Value |
| - | - | - |
| **Computer Configuration\Administrative Templates\System\Credentials Delegation** | Remote host allows delegation of nonexportable credentials | Enabled |

[!INCLUDE [gpo-settings-2](../../../includes/configure/gpo-settings-2.md)]

---


## Configure the lock screen background

You can use configuration service provider (CSP) or group policy (GPO) settings to configure access to the Microsoft Store app. The CSP configuration is available to Windows Enterprise and Education editions only.

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg" border="false"::: **Intune/CSP**](#tab/intune)

To configure the desktop background, you can use:

- Microsoft Intune/MDM
- Group policy
- Registry

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg" border="false"::: **Intune/CSP**](#tab/intune)

[!INCLUDE [intune-settings-catalog-1](../../../includes/configure/intune-settings-catalog-1.md)]

| Category | Setting name | Value |
|--|--|--|
| **Administrative Templates > System > Credentials Delegation** | Remote host allows delegation of nonexportable credentials | Enabled |

[!INCLUDE [intune-settings-catalog-2](../../../includes/configure/intune-settings-catalog-2.md)]

Alternatively, you can configure devices using a [custom policy][INT-3] with the [Policy CSP][CSP-1].

| Setting |
|--------|
| - **OMA-URI:** `./Device/Vendor/MSFT/Policy/Config/CredentialsDelegation/RemoteHostAllowsDelegationOfNonExportableCredentials`<br>- **Data type:** string<br>- **Value:** `<enabled/>`|

#### [:::image type="icon" source="../images/icons/group-policy.svg" border="false"::: **GPO**](#tab/gpo)

[!INCLUDE [gpo-settings-1](../../../includes/configure/gpo-settings-1.md)]

| Group policy path | Group policy setting | Value |
| - | - | - |
| **Computer Configuration\Administrative Templates\System\Credentials Delegation** | Remote host allows delegation of nonexportable credentials | Enabled |

[!INCLUDE [gpo-settings-2](../../../includes/configure/gpo-settings-2.md)]

---


To configure the lock screen and background images, use the [Personalization CSP][CSP-2].

|Policy name| CSP | GPO |
|-|-|-|
|[DesktopImageUrl](/windows/client-management/mdm/personalization-csp#desktopimageurl)|✅|✅|
|[LockScreenImageUrl](/windows/client-management/mdm/personalization-csp#lockscreenimageurl)|✅|✅|

> [!TIP]
> You also have the option to configure a custom lock screen image using [organizational messages in the Microsoft 365 admin center][M365-1].



## User experience

When Windows spotlight is enabled, devices apply a new image on the lock screen and in the background every day. The image is displayed in the background when the user signs in, and on the lock screen when the user locks the device. Users can still receive suggestions, fun facts, tips, or organizational messages. If you deploy a custom lock screen or background image, devices apply the custom image instead of the Windows spotlight image:



<!--links-->

[CSP-2]: /windows/client-management/mdm/personalization-csp
[M365-1]: /microsoft-365/admin/misc/organizational-messages-microsoft-365?view=o365-worldwide
