---
title: Configure the Windows Taskbar Pinned Apps with Policy Settings
description: Learn how to configure the applications pinned to the Windows taskbar.
ms.topic: how-to
ms.date: 04/03/2025
appliesto:
zone_pivot_groups: windows-versions-11-10
---

# Configure the applications pinned to the taskbar

The configuration of the applications pinned to the taskbar is done with the use of an XML file. This article describes how to create and deploy the XML configuration file.

> [!NOTE]
> If you're looking for OEM information, see the article [Customize the Taskbar][OEM-1].

To learn about all the policy settings to customize the taskbar layout and configure the taskbar behaviors, see [Taskbar policy settings](policy-settings.md).

## Before you begin

Here are some considerations before you start configuring the taskbar pinned applications:

::: zone pivot="windows-11"
- There's no limit to the number of apps that you can pin
- In the XML file, add apps using the Application User Model ID (AUMID), the Desktop Application ID, or the Desktop Application Link Path
- Some classic Windows applications are packaged differently than they were in previous versions of Windows, including Notepad and File Explorer. Make sure to enter the correct Application ID. To learn more, see [Find the Application User Model ID of an installed app](../store/find-aumid.md)
- If you specify an app to be pinned that isn't provisioned for the user on the device, the pinned icon doesn't appear on the taskbar
- The order of applications in the XML file dictates the order of pinned apps on the taskbar, from left to right. If the OS is configured to use a right-to-left language, then the taskbar order is reversed
- By default, any pins provisioned via policy settings are restored upon the next policy update cycle, even when users unpin them
  - On devices with [KBXYZ][KB-1] or later, users can unpin apps pinned via policy settings, if allowed by the policy. The pins won't be repinned during the next policy update cycle
- Applications can be pinned using the following methods:
  - Default Windows apps, pinned during the OS installation. For example: Microsoft Edge, File Explorer, and Store. These applications are pinned first (blue square)
  - Pinned manually by the user. These applications are pinned next to the default pinned apps (red circle)
  - Pinned via policy settings. These applications are pinned after the apps pinned manually by the user (green triangle)

:::image type="content" source="images/pin-layout-11.png" border="false" lightbox="images/pin-layout-11.png" alt-text="Screenshot of the taskbar with Windows default pinned apps, user pinned apps, and policy-pinned apps.":::

::: zone-end

::: zone pivot="windows-10"

- There's no limit to the number of apps that you can pin
- In the XML file, add apps using the Application User Model ID (AUMID), the Desktop Application ID, or the Desktop Application Link Path
- Some classic Windows applications are packaged differently than they were in previous versions of Windows, including Notepad and File Explorer. Make sure to enter the correct Application ID. To learn more, see [Find the Application User Model ID of an installed app](../store/find-aumid.md)
- If you specify an app to be pinned that isn't provisioned for the user on the device, the pinned icon doesn't appear on the taskbar
- The order of applications in the XML file dictates the order of pinned apps on the taskbar, from left to right. If the OS is configured to use a right-to-left language, then the taskbar order is reversed
- Applications can be pinned using the following methods:
  - Default Windows apps, pinned during the OS installation. For example: Microsoft Edge, File Explorer, and Store. These applications are pinned first (blue square)
  - Pinned manually by the user. These applications are pinned next to the default pinned apps (red circle)
  - Pinned via policy settings. These applications are pinned after the apps pinned manually by the user (green triangle)

:::image type="content" source="images/pin-layout-10.png" border="false" lightbox="images/pin-layout-10.png" alt-text="Screenshot of the taskbar with Windows default pinned apps, user pinned apps, and policy-pinned apps.":::

::: zone-end


## Configuration steps

The following steps describe how to configure the taskbar pinned applications using policy settings:

1. Create the XML file. You can start with the [XML example](#taskbar-layout) and modify it to meet your requirements
1. Edit the XML file to meet your requirements and save it
1. Deploy the XML file to devices using configuration service provider (CSP), provisioning packages (PPKG), or group policy (GPO)

### Taskbar configuration and policy refresh

Depending on the method you use to configure the taskbar, the configuration is reapplied at different intervals. When the taskbar configuration is reapplied, user changes are overwritten.

| Configuration method | Reapplied interval |
|--|--|
| Configuration service provider (CSP) | Every 8 hours or based on the [ConfigRefresh](/windows/client-management/mdm/dmclient-csp#deviceproviderprovideridconfigrefresh) interval. |
| Provisioning package (PPKG) | Each time the `explorer.exe` process restarts. |
| Group policy (GPO) | If a group policy changes. |

> [!NOTE]
> The use of the `Import-StartLayout` PowerShell cmdlet to provision the Taskbar layout is no longer supported in Windows 11.

::: zone pivot="windows-10"

>[!NOTE]
>If you use GPO and your configuration only contains a taskbar layout, the default Windows tile layout is applied and can't be changed by users. If you use GPO and your configuration includes taskbar and a full Start layout, users can only make changes to the taskbar. If you use Group Policy and your configuration includes taskbar and a partial Start layout, users can make changes to the taskbar and to tile groups not defined in the partial Start layout.
>
> For more information, see [Configure the Start menu](../start/index.md).

::: zone-end

## Taskbar layout

Here you can find an example of taskbar layout that you can use as a reference:

[!INCLUDE [example](includes/example.md)]

### Modify the configuration file

> [!IMPORTANT]
> The XML format must adhere to the [XML schema definition (XSD)](xsd.md).

You can change the apps pinned to the taskbar by modifying the `<TaskbarLayout>` node.

1. In the `<taskbar:TaskbarPinList>` node, add (or remove) the apps you want pinned. You can pin Universal Windows Platform (UWP) apps and desktop apps:
    - `<taskbar:UWA>`: Select this option for UWP apps. Add the *AUMID* of the UWP app
    - `<taskbar:DesktopApp>`: Select this option for desktop apps. Add the *Desktop Application ID* or the *Desktop Application Link Path* of the desktop app
1. In the `<CustomTaskbarLayoutCollection>` node, the apps you add are pinned after the default apps. If you want to remove the default apps, and only show the apps you add in the XML file, then add `PinListPlacement="Replace"`:
    - `<CustomTaskbarLayoutCollection>`: Keeps the default pinned apps. After the default apps, the apps you add are pinned
    - `<CustomTaskbarLayoutCollection PinListPlacement="Replace">`: Unpins the default apps. Only the apps you add are pinned. If you want to remove some of the default pinned apps, then add `PinListPlacement="Replace"`. When you add your apps to `<taskbar:TaskbarPinList>`, include the default apps you still want pinned
1. In the `<defaultlayout:TaskbarLayout>` node, use `region=" | "` to use different taskbar configurations based on the device locale and region
1. Save the file

::: zone pivot="windows-11"

#### PinGeneration

On devices with [KBXYZ][KB-1] or later, you can allow specific pinned apps to be unpinnable by users. This is useful when you want to allow users to unpin apps that are pinned via policy settings, but you don't want the pins to be repinned during the next policy update cycle.

To use this option, add `PinGeneration="1"` to the pins you want to allow users to unpin. The value of `PinGeneration` can be any number, and it's used to identify the pin version. If the value changes, the app is pinned again during the next policy update cycle. This allows IT admins to repin an app, if needed.

Here are some details to better understand and use `PinGeneration`:

- When `PinGeneration` isn't defined, users can unpin that element, but the pin is repinned during the next policy update cycle
- When `PinGeneration` is defined, users can unpin that element, and the pin isn't repinned during the next policy update cycle
- When the `PinGeneration` value changes, for example from `1` to `2`, the element is pinned again, even if the user unpinned it previously
- Every `PinGeneration` number is specific to an app. You can define a value of `1` for one app, and a value of `2` for another app
- Start `PinGeneration` with a value of `1` and increment the number each time you want to repin the app. This way, if the user unpins the app, it's not repinned until you change the number again
- For simple management, always increment the `PinGeneration` number and don't reuse numbers
- If you remove the `PinGeneration` attribute, the app is repinned during the next policy update cycle even if the user unpinned it previously. This is the default behavior

> [!CAUTION]
> The `PinGeneration` option is only available on devices with [KBXYZ][KB-1] or later. Only assign this policy to devices that are patched, otherwise the taskbar pins don't apply.
>
>- With Microsoft Intune you can use [filters](/intune/intune-service/fundamentals/filters) to target only devices with the required patch
>- With GPO you can use [WMI filters](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732796(v=ws.11)) to target only devices with the required patch

::: zone-end

## Examples

For practical examples of how to add, remove, or replace pinned apps, see the following sections:

::: zone pivot="windows-10"

- [Add pins](#example-add-pins)
- [Remove default pins](#example-remove-pins)
- [Replace default pins](#example-replace-pins)
- [Configure the taskbar by country or region](#example-configure-the-taskbar-by-country-or-region)

::: zone-end

::: zone pivot="windows-11"

- [Add pins](#example-add-pins)
- [Remove default pins](#example-remove-pins)
- [Replace default pins](#example-replace-pins)
- [Allow unpinning of specific apps](#example-allow-unpinning-of-specific-apps)
- [Configure the taskbar by country or region](#example-configure-the-taskbar-by-country-or-region)

::: zone-end

#### Example: add pins

The `<CustomTaskbarLayoutCollection>` section appends the listed apps to the taskbar by default. The following sample keeps the default apps pinned and adds pins for Paint, Microsoft Reader, and a command prompt.

[!INCLUDE [example-add-pins](includes/example-add-pins.md)]

**Before and after:**

::: zone pivot="windows-11"
:::image type="content" source="images/pin-add-11.png" alt-text="Screenshot of the Windows 11 taskbar, before and after adding pins." border="false" lightbox="./images/pin-add-11.png":::
::: zone-end

::: zone pivot="windows-10"
:::image type="content" source="images/pin-add-10.png" alt-text="Screenshot of the Windows 10 taskbar, before and after adding pins." border="false" lightbox="./images/pin-add-10.png":::
::: zone-end

#### Example: remove pins

To remove all pins, add `PinListPlacement="Replace"` to `<CustomTaskbarLayoutCollection>`.

[!INCLUDE [example-remove-pins](includes/example-remove-pins.md)]

**Before and after:**

::: zone pivot="windows-11"
:::image type="content" source="images/pin-remove-11.png" alt-text="Screenshot of the Windows 11 taskbar, before and after removing pins." border="false" lightbox="images/pin-remove-11.png":::
::: zone-end

::: zone pivot="windows-10"
:::image type="content" source="images/pin-remove-10.png" alt-text="Screenshot of the Windows 10 taskbar, before and after removing pins." border="false" lightbox="images/pin-remove-10.png":::
::: zone-end

#### Example: replace pins

To replace all default pins and add your own pins, add `PinListPlacement="Replace"` to `<CustomTaskbarLayoutCollection>`. Then, add the pins that you want to `TaskbarPinList`.

[!INCLUDE [example-replace-pins](includes/example-replace-pins.md)]

**Before and after:**

::: zone pivot="windows-11"
:::image type="content" source="images/pin-replace-11.png" alt-text="Screenshot of the Windows 11 taskbar, before and after replacing pins." border="false" lightbox="images/pin-replace-11.png":::
::: zone-end

::: zone pivot="windows-10"
:::image type="content" source="images/pin-replace-10.png" alt-text="Screenshot of the Windows 10 taskbar, before and after replacing pins." border="false" lightbox="images/pin-replace-10.png":::
::: zone-end

::: zone pivot="windows-11"

#### Example: allow unpinning of specific apps

> [!NOTE]
> The option to allow users to unpin apps is only available on devices with [KBXYZ][KB-1] or later.

"In the following XML example, three apps are pinned to the taskbar. Two apps are pinned with the `PinGeneration` attribute, allowing users to unpin them and preventing repinning during the next policy update cycle.

[!INCLUDE [example-replace-pins](includes/example-add-pins-pingeneration.md)]

**Before and after:**

:::image type="content" source="images/pin-add-pingeneration-11.png" alt-text="Screenshot of the Windows 11 taskbar, before and after adding pins with the Microsoft 365 companion apps." border="false" lightbox="images/pin-add-pingeneration-11.png":::

::: zone-end

#### Example: configure the taskbar by country or region

In the following XML example, two regions are added: `US|UK` and `DE|FR|IT`:

[!INCLUDE [example](includes/example-region.md)]

- If the `<TaskbarPinList>` node has region matching the one configured on the device, then the configuration applies
- If the `<TaskbarPinList>` node doesn't have a region matching the one configured on the device, then the first `<TaskbarPinList>` node without region applies

> [!NOTE]
> [Look up country and region codes (use the ISO Short column)](/previous-versions/commerce-server/ee799297(v=cs.20))

## Deploy the taskbar configuration

[!INCLUDE [tab-intro](../../../includes/configure/tab-intro.md)]

#### [:::image type="icon" source="../images/icons/intune.svg"::: **Intune**](#tab/intune)

To configure devices with Microsoft Intune, [create a Settings catalog policy](/mem/intune/configuration/settings-catalog) and use one of the following settings:

| Category | Setting name | Value |
|--|--|--|
| **Start** | Start Layout | Content of the XML file|
| **Start** | Start Layout (User) | Content of the XML file|

[!INCLUDE [intune-settings-catalog-2](../../../includes/configure/intune-settings-catalog-2.md)]

#### [:::image type="icon" source="../images/icons/csp.svg"::: **CSP**](#tab/csp)

You can configure devices using the [Start CSP][WIN-1]. Use one of the following settings:

| Setting |
|--|
| - **OMA-URI:** `./User/Vendor/MSFT/Policy/Config/Start/`[StartLayout](/windows/client-management/mdm/policy-csp-Start#startlayout)<br>- **Data type:** String <br>- **Value:** content of the XML file |
| - **OMA-URI:** `./Device/Vendor/MSFT/Policy/Config/Start/`[StartLayout](/windows/client-management/mdm/policy-csp-Start#startlayout)<br>- **Data type:** String <br>- **Value:** content of the XML file |

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

[!INCLUDE [provisioning-package-1](../../../includes/configure/provisioning-package-1.md)]

- **Path:** `Policies/Start/StartLayout`
- **Value:** content of the XML file

> [!NOTE]
> The content of the file must be entered as a single line in the `Value` field. Use a text editor to remove any line breaks from the XML file, usually with a function called *join lines* or *linearize*. If customizations.xml is being modified directly instead of using the WCD editor, the XML brackets need to be escaped / replaced with \&lt; and \&gt; entity encodings. Single and double quote characters don't need to be escaped.

[!INCLUDE [provisioning-package-2](../../../includes/configure/provisioning-package-2.md)]

#### [:::image type="icon" source="../images/icons/group-policy.svg"::: **GPO**](#tab/gpo)

To configure a device with group policy, use the [Local Group Policy Editor](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731745(v=ws.10)). To configure multiple devices joined to Active Directory, [create or edit](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc754740(v=ws.11)) a group policy object (GPO) and use one of the following settings:

| Group policy path | Group policy setting | Value |
| - | - | - |
|**Computer Configuration** > **Administrative Templates** > **Start Menu and Taskbar**| Start Layout | Path to the XML file |
|**User Configuration** > **Administrative Templates** > **Start Menu and Taskbar**| Start Layout | Path to the XML file |

[!INCLUDE [gpo-settings-2](../../../includes/configure/gpo-settings-2.md)]

The GPO applies the Start and taskbar layout at the next user sign-in. Each time the user signs in, the timestamp of the .xml file with the Start and taskbar layout is checked and if a newer version of the file is available, the settings in the latest version of the file are applied.

---

## User experience

::: zone pivot="windows-10"
After the taskbar layout is applied, users must sign out and sign in again to get the new layout. Unless prohibited via policy settings, users can add pins, remove pins, and change their order.

Any pins provisioned via policy settings are restored upon the next policy refresh, even when users unpin them.
::: zone-end

::: zone pivot="windows-11"
After the taskbar layout is applied, users must sign out and sign in again to get the new layout. Unless prohibited via policy settings, users can add pins, remove pins, and change their order.

- By default, any pins provisioned via policy settings are restored upon the next policy update cycle, even when users unpin them
- Pins defined with the `PinGeneration` attribute can be unpinned from the taskbar, and aren't repinned during the next policy update cycle

::: zone-end

### OS install and upgrade experience

On a clean install of Windows, if you apply a taskbar layout, the following apps are pinned to the taskbar:

- Any default apps you don't remove
- Apps that you specifically pin in the XML file

On a Windows OS upgrade, apps are already pinned to the taskbar. The taskbar layout applies the following logic:

- If users pinned elements to the taskbar, then those items remain. New pins appear after the existing user-pinned elements
- If the apps are pinned during the install or by a policy (not by a user), and the apps aren't pinned in an updated layout file, then the apps are unpinned
- If a user didn't pin an app, and the same app is pinned in the updated layout file, then the app is pinned after any existing pinned apps
- New apps in updated layout file are pinned after the user's pinned apps

If you apply the taskbar configuration to a clean install or an update, users can still:

- Pin more apps
- Change the order of pinned apps
- Unpin any app

## Next steps

Learn more about the options available to configure Start menu settings using the Configuration Service Provider (CSP) and Group Policy (GPO):

- [Taskbar policy settings](policy-settings.md)

<!--links-->

[OEM-1]: /windows-hardware/customize/desktop/customize-the-windows-11-taskbar
[WIN-1]: /windows/client-management/mdm/policy-csp-start
[MEM-1]: /mem/intune/configuration/custom-settings-windows-10
[KB-1]: /windows/