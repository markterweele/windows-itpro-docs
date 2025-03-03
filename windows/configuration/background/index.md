---
title: Configure the Background in Windows
description: Learn how to configure the background in Windows for managed devices, using policy settings, including Intune, CSP and GPO.
ms.topic: how-to
ms.date: 03/03/2025
author: paolomatarazzo
ms.author: paoloma
appliesto:
zone_pivot_groups: windows-versions-11-10
---

# Configure the background in Windows

You can replace the Windows spotlight lock screen and background images with a custom image. When you do so, users can still see suggestions, fun facts, tips, or organizational messages on the lock screen, but the background image is replaced with the custom image.

To configure the lock screen and background images, use the [Personalization CSP][CSP-2].

|Policy name| CSP | GPO |
|-|-|-|
|[DesktopImageUrl](/windows/client-management/mdm/personalization-csp#desktopimageurl)|✅|✅|
|[LockScreenImageUrl](/windows/client-management/mdm/personalization-csp#lockscreenimageurl)|✅|✅|

>[!NOTE]
> A concern with custom images is how they'll appear on different screen sizes and resolutions. A custom image created in `16:9` aspect ratio (for example, `1600x900`) scales properly on devices using a `16:9` resolution, such as `1280x720` or `1920x1080`. On devices using other aspect ratios, such as `4:3` (`1024x768`) or `16:10` (`1280x800`), height scales correctly and width is cropped to a size equal to the aspect ratio. The image remains centered on the screen.
>
> Lock screen images created at other aspect ratios might scale and center unpredictably on your device when changing aspect ratios. The recommendation for custom images that include text (such as a legal statement), is to create the lock screen image in `16:9` resolution with text contained in the `4:3` region, allowing the text to remain visible at any aspect ratio.

> [!TIP]
> You also have the option to configure a custom lock screen image using [organizational messages in the Microsoft 365 admin center][M365-1].

## User experience

When Windows spotlight is enabled, devices apply a new image on the lock screen and in the background every day. The image is displayed in the background when the user signs in, and on the lock screen when the user locks the device. Users can still receive suggestions, fun facts, tips, or organizational messages. If you deploy a custom lock screen or background image, devices apply the custom image instead of the Windows spotlight image:

::: zone pivot="windows-11"

:::image type="content" source="images/contoso-lockscreen-11.png" alt-text="Screenshot of the Windows 11 lock screen with Windows spotlight enabled over an organization wallpaper." border="false":::

::: zone-end

::: zone pivot="windows-10"

:::image type="content" source="images/contoso-lockscreen-10.png" alt-text="Screenshot of the Windows 10 lock screen with Windows spotlight enabled over an organization wallpaper." border="false":::

::: zone-end

<!--links-->

[CSP-2]: /windows/client-management/mdm/personalization-csp
[M365-1]: /microsoft-365/admin/misc/organizational-messages-microsoft-365?view=o365-worldwide
