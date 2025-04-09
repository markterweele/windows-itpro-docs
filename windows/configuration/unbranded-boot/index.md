---
title: Unbranded Boot
description: Learn about Unbranded Boot, a feature that suppresses Windows elements that appear when Windows starts. Unbranded Boot can also suppress the crash screen when Windows encounters an error that it can't recover from.
ms.date: 04/09/2025
ms.topic: how-to
---

# Unbranded Boot

Unbranded Boot is a Windows feature that allows you to suppress Windows elements that appear when Windows starts. It can also suppress the crash screen when Windows encounters an error that it can't recover from. This feature is useful for devices that are used in public spaces, such as kiosks and digital signs, where a clean and professional appearance is important.

[!INCLUDE [unbranded-boot](../../../includes/licensing/unbranded-boot.md)]

## Enable Unbranded Boot

> [!IMPORTANT]
> The first user to sign in to the device must be an administrator. This ensures that the **RunOnce** registry settings correctly apply the settings. Also, when using auto sign-in, you must not configure auto sign-in on your device at design time. Instead, auto sign-in should be configured manually after first signing in as an administrator.

Unbranded Boot is an optional component and isn't enabled by default in Windows. It must be enabled prior to configuring.

If Windows is already installed, you can't apply a provisioning package to configure Unbranded Boot. You must use the Boot Configuration Data Editor (`bcdedit.exe`) to configure Unbranded Boot if Windows is installed.

> [!NOTE]
> `Bcdedit.exe` is a command-line tool for editing the Boot Configuration Data (BCD) of Windows. Administrator privileges are required to use BCDEdit to modify the BCD.

### Turn on Unbranded Boot by using Control Panel

1. In the Windows search bar, type **Turn Windows features on or off** and either press **Enter** or tap or select **Turn Windows features on or off** to open the **Windows Features** window
1. In the **Windows Features** window, expand the **Device Lockdown** node, and select (to turn on) or clear (to turn off) the checkbox for **Unbranded Boot**
1. Select **OK**. The **Windows Features** window indicates that Windows is searching for required files and displays a progress bar. Once found, the window indicates that Windows is applying the changes. When completed, the window indicates the requested changes are completed
1. Restart your device to apply the changes

## Configure Unbranded Boot

The following instructions provide details about how to configure your devices. Select the option that best suits your needs.

#### [:::image type="icon" source="../images/icons/cmd.svg"::: **Command prompt**](#tab/cmd)

You can use the `bcdedit.exe` command to configure Unbranded Boot settings at runtime.

1. Open a command prompt as an administrator
1. Run the following command to disable the F8 key during startup to prevent access to the **Advanced startup options** menu

   ```cmd
   bcdedit.exe -set {globalsettings} advancedoptions false
   ```

1. Run the following command to disable the F10 key during startup to prevent access to the **Advanced startup options** menu

   ```cmd
   bcdedit.exe -set {globalsettings} optionsedit false
   ```

1. Run the following command to suppress all Windows UI elements (logo, status indicator, and status message) during startup

   ```cmd
   bcdedit.exe -set {globalsettings} bootuxdisabled on
   ```

1. Run the following command to suppress any error screens that are displayed during boot. If **noerrordisplay** is on and the boot manager hits a *WinLoad Error* or *Bad Disk Error*, the system displays a black screen

   ```cmd
   bcdedit.exe -set {bootmgr} noerrordisplay on
   ```

#### [:::image type="icon" source="../images/icons/xml.svg"::: **Unattend**](#tab/unattend)

You can configure the Unattend settings in the `Microsoft-Windows-Embedded-BootExp` component to add Unbranded Boot features to your image during the design or imaging phase. You can manually create an Unattend answer file or use Windows System Image Manager (Windows SIM) to add the appropriate settings to your answer file. For more information about the Unbranded Boot settings and XML examples, see the settings in [Microsoft-Windows-Embedded-BootExp](/windows-hardware/customize/desktop/unattend/microsoft-windows-embedded-bootexp).

### Unbranded Boot settings

The following table lists Unbranded Boot settings and their values.

| Setting | Description | Value |
|---------|-------------|-------|
| `DisableBootMenu` | Contains an integer that disables the F8 and F10 keys during startup to prevent access to the *Advanced startup options* menu. | - Set to `1` to disable the menu<br>- The default value is `0`|
| `DisplayDisabled` | Contains an integer that configures the device to display a blank screen when Windows encounters an error that it can't recover from. | - Set to `1` to display a blank screen on error<br>- The default value is `0`|
| `HideAllBootUI` | Contains an integer that suppresses all Windows UI elements (logo, status indicator, and status message) during startup. | - Set to `1` to suppress all Windows UI elements during startup<br>- The default value is `0`|
| `HideBootLogo` | Contains an integer that suppresses the default Windows logo that displays during the OS loading phase. | - Set to `1` to suppress the default Windows logo<br>- The default value is `0`|
| `HideBootStatusIndicator` | Contains an integer that suppresses the status indicator that displays during the OS loading phase. | - Set to `1` to suppress the status indicator<br>- The default value is `0`|
| `HideBootStatusMessage` | Contains an integer that suppresses the startup status text that displays during the OS loading phase. | - Set to `1` to suppress the startup status text<br>- The default value is `0`|

#### [:::image type="icon" source="../images/icons/provisioning-package.svg"::: **PPKG**](#tab/ppkg)

Customize the boot screen using Windows Configuration Designer and Deployment Image Servicing and Management (DISM).

You must enable Unbranded Boot on the installation media with DISM before you can apply settings for Unbranded Boot using either Windows Configuration Designer or applying a provisioning package during setup.

[!INCLUDE [provisioning-package-1](../../../includes/configure/provisioning-package-1.md)]

|Path|Value|
|---|---|
|`Runtime settings/SMISettings/HideAllBootUI`| `TRUE` or `FALSE`|
|`Runtime settings/SMISettings/HideBootLogo`| `TRUE` or `FALSE`|
|`Runtime settings/SMISettings/HideBootStatusIndicator`| `TRUE` or `FALSE`|
|`Runtime settings/SMISettings/HideBootStatusMessage`| `TRUE` or `FALSE`|
|`Runtime settings/SMISettings/CrashDumpEnabled`| `Full dump`|

[!INCLUDE [provisioning-package-2](../../../includes/configure/provisioning-package-2.md)]

   > [!TIP]
   > For more information, see [SMISettings](/windows/configuration/wcd/wcd-smisettings) in the Windows Configuration Designer reference.

1. Once you have finished configuring the settings and building the package or image, you use DISM to apply the settings.
   1. Open a command prompt with administrator privileges.
   1. Copy install.wim to a temporary folder on hard drive (in the following steps, it assumes it's called c:\\wim).
   1. Create a new directory.

      ```cmd
      md c:\wim
      ```

   1. Mount the image.

      ```cmd
      dism /mount-wim /wimfile:c:\bootmedia\sources\install.wim /index:1 /MountDir:c:\wim
      ```

   1. Enable the feature.

      ```cmd
      dism /image:c:\wim /enable-feature /featureName:Client-EmbeddedBootExp
      ```

   1. Commit the change.

      ```cmd
      dism /unmount-wim /MountDir:c:\wim /Commit
      ```

In the following image, the BootLogo is outlined in green, the BootStatusIndicator is outlined in red, and the BootStatusMessage is outlined in blue.

---

![Unbranded Boot screen](images/boot.jpg)

## Replace the startup logo

The only supported way to replace the startup logo with a custom logo is to modify the Boot Graphics Resource Table (BGRT) on a device that uses UEFI as the firmware interface. If your device uses the BGRT to include a custom logo, it's always displayed and you can't suppress the custom logo.
