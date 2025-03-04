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

This article explains how to configure the desktop and lock screen background in Windows using policy settings. It includes examples of how to implement these configurations using Microsoft Intune, Configuration Service Provider (CSP), and Group Policy Object (GPO).

## Image ratios and scaling

A key consideration when using custom images is how they appear on devices with varying screen sizes and resolutions. For example, a custom image created in a 16:9 aspect ratio (such as 1600x900) scales properly on devices with 16:9 resolutions, like 1280x720 or 1920x1080. On devices with other aspect ratios, such as 4:3 (1024x768) or 16:10 (1280x800), the image's height scales correctly, but the width is cropped to match the aspect ratio. The image remains centered on the screen.

Images created in non-standard aspect ratios may scale and center unpredictably when displayed on devices with different resolutions. To ensure consistent results, especially for images containing text (e.g., legal statements), it is recommended to design the image in a 16:9 resolution while keeping critical text within the 4:3 region. This approach ensures that the text remains visible across all aspect ratios.

## Configure the desktop background

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

When the policy is applied, the lock screen and desktop background images are set to the specified URL. The images are downloaded and cached locally on the device. The images are displayed in the background when the user signs in, and on the lock screen when the user locks the device.

## Windows spotlight

Windows Spotlight is a feature that displays beautiful images on the lock screen and desktop background. It can be configured to show different images each day, or to display a specific image. Windows Spotlight can also provide personalized content, such as tips and tricks for using Windows. To learn more about Windows Spotlight, see [Windows Spotlight for Business](https://learn.microsoft.com/windows/configuration/windows-spotlight-business).

<!--links-->

[CSP-2]: /windows/client-management/mdm/personalization-csp
[M365-1]: /microsoft-365/admin/misc/organizational-messages-microsoft-365?view=o365-worldwide
[INT-3]: /mem/intune/configuration/settings-catalog
