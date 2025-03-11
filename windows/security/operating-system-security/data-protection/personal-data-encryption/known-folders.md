---
title: Personal Data Encryption For Known Folders
description: Learn about Personal Data Encryption for known folders and how to configure it via Microsoft Intune and Configuration Service Providers (CSP).
ms.topic: how-to
ms.date: 09/24/2024
---

# Personal Data Encryption for know folders

Starting in Windows 11, version 24H2, Personal Data Encryption is further enhanced with Personal Data Encryption for known folders, which extends protection to the Windows folders: **Desktop**, **Documents**, and **Pictures**.

:::image type="content" source="images/known-folders-pde.png" alt-text="Icons of the known folders with a padlock representing their encryption status.":::

## Personal Data Encryption for know folders settings

The following table lists the settings to configuire Personal Data Encryption for know folders.

| Setting name | Description |
|-|-|
|Enable Personal Data Encryption|Personal Data Encryption isn't enabled by default. Before Personal Data Encryption can be used, you must enable it.|
|Sign-in and lock last interactive user automatically after a restart| Winlogon automatic restart sign-on (ARSO) isn't supported for use with Personal Data Encryption. To use Personal Data Encryption, ARSO must be disabled.|

## Configure Personal Data Encryption for know folders

[!INCLUDE [intune-settings-catalog-1](../../../../../includes/configure/intune-settings-catalog-1.md)]

| Category | Setting name | Value |
|--|--|--|
|  |  |  |

[!INCLUDE [intune-settings-catalog-2](../../../../includes/configure/intune-settings-catalog-2.md)]

Alternatively, you can configure devices using a [custom policy][INT-1] with the [DeviceGuard Policy CSP][CSP-1].

| Setting |
|--------|
| **Setting name**: <br>**OMA-URI**: ``<br>**Data type**: int<br>**Value**: `1`|
| **Setting name**: <br>**OMA-URI**: ``<br>**Data type**: int<br>**Value**:<br>&emsp;**Enabled with UEFI lock**: `1`<br>&emsp;**Enabled without lock**: `2`|


If you use Microsoft Intune to manage your devices, you can configure Personal Data Encryption using a disk encryption policy, a settings catalog policy, or a custom profile.

### Disk encryption policy

To configure devices using a [disk encryption policy](/mem/intune/protect/endpoint-security-disk-encryption-policy), go to **Endpoint security** > **Disk encryption** and select **Create policy**:

- **Platform** > **Windows**
- **Profile** > **Personal Data Encryption**

Provide a name, and select **Next**. In the **Configuration settings** page, select **Enable Personal Data Encryption** and configure the settings as needed.

Assign the policy to a group that contains as members the devices or users that you want to configure.

### Settings catalog policy

[!INCLUDE [intune-settings-catalog-1](../../../../../includes/configure/intune-settings-catalog-1.md)]

| Category | Setting name | Value |
|--|--|--|
|**PDE**|Enable Personal Data Encryption (User)|Enable Personal Data Encryption|
|**Administrative Templates > Windows Components > Windows Logon Options**|Sign-in and lock last interactive user automatically after a restart|Disabled|
|**Memory Dump**|Allow Live Dump|Block|
|**Memory Dump**|Allow Crash Dump|Block|
|**Administrative Templates > Windows Components > Windows Error Reporting** | Disable Windows Error Reporting | Enabled|
|**Power**|Allow Hibernate|Block|
|**Administrative Templates > System > Logon** | Allow users to select when a password is required when resuming from connected standby | Disabled|

[!INCLUDE [intune-settings-catalog-2](../../../../../includes/configure/intune-settings-catalog-2.md)]

> [!TIP]
> Use the following Graph call to automatically create the settings catalog policy in your tenant without assignments nor scope tags.
>
> When using this call, authenticate to your tenant in the Graph Explorer window. If it's the first time using Graph Explorer, you may need to authorize the application to access your tenant or to modify the existing permissions. This graph call requires *DeviceManagementConfiguration.ReadWrite.All* permissions.

## Configure Personal Data Encryption with CSP

Alternatively, you can configure devices using the [Policy CSP][CSP-1] and [Personal Data Encryption CSP][CSP-2].

|OMA-URI|Format|Value|
|-|-|-|
|`./User/Vendor/MSFT/PDE/EnablePersonalDataEncryption`|int|`1`|
|`./Device/Vendor/MSFT/Policy/Config/WindowsLogon/AllowAutomaticRestartSignOn`|string|`<disabled/>`|
|`./Device/Vendor/MSFT/Policy/Config/MemoryDump/AllowCrashDump`| int| `0`|
|`./Device/Vendor/MSFT/Policy/Config/MemoryDump/AllowLiveDump` |int| `0`|
|`./Device/Vendor/MSFT/Policy/Config/ErrorReporting/DisableWindowsErrorReporting`|string|`<enabled/>`|
|`./Device/Vendor/MSFT/Policy/Config/Power/AllowHibernate` |int| `0`|
|`./Device/Vendor/MSFT/Policy/Config/ADMX_CredentialProviders/AllowDomainDelayLock`|string|`<disabled/>`|

## User experience

When Personal Data Encryption is enabled, the user experience is as follows:

<!--links used in this document-->

[CSP-1]: /windows/client-management/mdm/policy-configuration-service-provider
[CSP-2]: /windows/client-management/mdm/personaldataencryption-csp
