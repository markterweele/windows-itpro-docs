---
title: User Account Control settings and configuration
description: Learn about the User Account Control settings and how to configure them via Intune, CSP, group policy, and registry.
ms.date: 04/15/2025
ms.topic: how-to
---

# User Account Control settings and configuration

## User Account Control settings list

The following list shows the available settings to configure the UAC behavior, and their default values.

- **Admin Approval Mode for the built-in Administrator account**: Controls the behavior of Admin Approval Mode for the built-in Administrator account.
    - **Enabled**: The built-in Administrator account uses Admin Approval Mode. By default, any operation that requires elevation of privilege prompts the user to prove the operation.
    - **Disabled (default)**: The built-in Administrator account runs all applications with full administrative privilege.

- **Allow UIAccess applications to prompt for elevation without using the secure desktop**: Controls whether User Interface Accessibility (UIAccess or UIA) programs can automatically disable the secure desktop for elevation prompts used by a standard user.
    - **Enabled**: UIA programs, including Remote Assistance, automatically disable the secure desktop for elevation prompts. If you don't disable the **Switch to the secure desktop when prompting for elevation** policy setting, the prompts appear on the interactive user's desktop instead of the secure desktop. This setting allows the remote administrator to provide the appropriate credentials for elevation. This policy setting doesn't change the behavior of the UAC elevation prompt for administrators. If you plan to enable this policy setting, you should also review the effect of the **Behavior of the elevation prompt for standard users** policy setting; if configured as **Automatically deny elevation requests**, elevation requests aren't presented to the user.
    - **Disabled (default)**: The secure desktop can be disabled only by the user of the interactive desktop or by disabling the **Switch to the secure desktop when prompting for elevation** policy setting.

- **Behavior of the elevation prompt for administrators in Admin Approval Mode**: Controls the behavior of the elevation prompt for administrators.
    - **Elevate without prompting**: Allows privileged accounts to perform an operation that requires elevation without requiring consent or credentials. **Use this option only in the most constrained environments**.
    - **Prompt for credentials on the secure desktop**: When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a privileged user name and password. If the user enters valid credentials, the operation continues with the user's highest available privilege.
    - **Prompt for consent on the secure desktop**: When an operation requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.
    - **Prompt for credentials**: When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.
    - **Prompt for consent**: When an operation requires elevation of privilege, the user is prompted to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.
    - **Prompt for consent for non-Windows binaries (default)**: When an operation for a non-Microsoft application requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

- **Behavior of the elevation prompt for standard users**: Controls the behavior of the elevation prompt for standard users.
    - **Prompt for credentials (default)**: When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.
    - **Automatically deny elevation requests**: When an operation requires elevation of privilege, a configurable access denied error message is displayed. An enterprise that is running desktops as standard user might choose this setting to reduce help desk calls.
    - **Prompt for credentials on the secure desktop**: When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a different user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

- **Detect application installations and prompt for elevation**: Controls the behavior of application installation detection for the computer.
    - **Enabled (default)**: When an app installation package is detected that requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.
    - **Disabled**: App installation packages aren't detected and prompted for elevation. Enterprises that are running standard user desktops and use delegated installation technologies, such as Microsoft Intune, should disable this policy setting. In this case, installer detection is unnecessary.

- **Only elevate executables that are signed and validated**: Enforces signature checks for any interactive applications that request elevation of privilege. IT admins can control which applications are allowed to run by adding certificates to the Trusted Publishers certificate store on local devices.
    - **Enabled**: Enforces the certificate certification path validation for a given executable file before it's permitted to run.
    - **Disabled (default)**: Doesn't enforce the certificate certification path validation before a given executable file is permitted to run.

- **Only elevate UIAccess applications that are installed in secure locations**: Controls whether applications that request to run with a User Interface Accessibility (UIAccess) integrity level must reside in a secure location in the file system.

    - **Enabled (default)**: If an app resides in a secure location in the file system, it runs only with UIAccess integrity.
    - **Disabled**: An app runs with UIAccess integrity even if it doesn't reside in a secure location in the file system.

    Secure locations are limited to the following folders:
    - `%ProgramFiles%`, including subfolders
    - `%SystemRoot%\system32\`
    - `%ProgramFiles(x86)%`, including subfolders

    > [!NOTE]
    > Windows enforces a digital signature check on any interactive apps that request to run with a UIAccess integrity level regardless of the state of this setting.

- **Run all administrators in Admin Approval Mode**: Controls the behavior of all UAC policy settings.
    - **Enabled (default)**: Admin Approval Mode is enabled. This policy must be enabled and related UAC settings configured. The policy allows the built-in Administrator account and members of the Administrators group to run in Admin Approval Mode.
    - **Disabled**: Admin Approval Mode and all related UAC policy settings are disabled. **Note:** If this policy setting is disabled, **Windows Security** notifies you that the overall security of the operating system is reduced.

- **Switch to the secure desktop when prompting for elevation**: This policy setting controls whether the elevation request prompt is displayed on the interactive user's desktop or the secure desktop.
    - **Enabled (default)**: All elevation requests go to the secure desktop regardless of prompt behavior policy settings for administrators and standard users.
    - **Disabled**: All elevation requests go to the interactive user's desktop. Prompt behavior policy settings for administrators and standard users are used.

- **Virtualize File And Registry Write Failures To Per User Locations**: Controls whether application write failures are redirected to defined registry and file system locations. This setting mitigates applications that run as administrator and write run-time application data to `%ProgramFiles%`, `%Windir%`, `%Windir%\system32`, or `HKLM\Software`.
    - **Enabled (default)**: App write failures are redirected at run time to defined user locations for both the file system and registry.
    - **Disabled**: Apps that write data to protected locations fail.

## User Account Control configuration

To configure UAC, you can use:

- Microsoft Intune
- CSP
- Group policy
- Registry

The following instructions provide details how to configure your devices. Select the option that best suits your needs.

#### [:::image type="icon" source="../../../images/icons/intune.svg"::: **Intune**](#tab/intune)

To configure devices using Microsoft Intune, [create a **Settings catalog** policy][MEM-2], and use the settings listed under the category **`Local Policies Security Options`**:

:::image type="content" source="images/uac-settings-catalog.png" alt-text="Screenshot that shows the UAC policies in the Intune settings catalog." lightbox="images/uac-settings-catalog.png" border="True":::

Assign the policy to a security group that contains as members the devices or users that you want to configure.

#### [:::image type="icon" source="../../../images/icons/csp.svg"::: **CSP**](#tab/csp)

You can configure devices using the [LocalPoliciesSecurityOptions Policy CSP][WIN-1].

|Setting|CSP Name|
|--|--|
| Admin Approval Mode for the built-in Administrator account |  `UserAccountControl_UseAdminApprovalMode`|
| Allow UIAccess applications to prompt for elevation without using the secure desktop | `UserAccountControl_AllowUIAccessApplicationsToPromptForElevation` |
| Behavior of the elevation prompt for administrators in Admin Approval Mode |  `UserAccountControl_BehaviorOfTheElevationPromptForAdministrators`|
| Behavior of the elevation prompt for standard users | `UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers`|
| Detect application installations and prompt for elevation | `UserAccountControl_DetectApplicationInstallationsAndPromptForElevation`|
| Only elevate executables that are signed and validated | `UserAccountControl_OnlyElevateExecutableFilesThatAreSignedAndValidated`|
| Only elevate UIAccess applications that are installed in secure locations | `UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations`|
| Run all administrators in Admin Approval Mode | `UserAccountControl_RunAllAdministratorsInAdminApprovalMode`|
| Switch to the secure desktop when prompting for elevation | `UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation`|
| Virtualize file and registry write failures to per-user locations | `UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations`|


#### [:::image type="icon" source="../../../images/icons/group-policy.svg" border="false"::: **GPO**](#tab/gpo)

You can use security policies to configure how User Account Control works in your organization. The policies can be configured locally by using the Local Security Policy snap-in (`secpol.msc`) or configured for the domain, OU, or specific groups by group policy.

The policy settings are located under: `Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options`.

| Group Policy setting                                                                                       | Default value                                                   |
|------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| User Account Control: Admin Approval Mode for the built-in Administrator account                           | Disabled                                                        |
| User Account Control: Allow UIAccess applications to prompt for elevation without using the secure desktop | Disabled                                                        |
| User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode           | Prompt for consent for non-Windows binaries                     |
| User Account Control: Behavior of the elevation prompt for standard users                                  | Prompt for credentials                                          |
| User Account Control: Detect application installations and prompt for elevation                            | Enabled (default for home edition only)<br />Disabled (default) |
| User Account Control: Only elevate executables that are signed and validated                               | Disabled                                                        |
| User Account Control: Only elevate UIAccess applications that are installed in secure locations            | Enabled                                                         |
| User Account Control: Run all administrators in Admin Approval Mode                                        | Enabled                                                         |
| User Account Control: Switch to the secure desktop when prompting for elevation                            | Enabled                                                         |
| User Account Control: Virtualize file and registry write failures to per-user locations                    | Enabled                                                         |

#### [:::image type="icon" source="../../../images/icons/registry.svg" border="false"::: **Registry**](#tab/reg)

The registry keys are found under the key: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`.

| Setting name | Registry key name | Value |
| - | - | - |
| Admin Approval Mode for the built-in Administrator account | `FilterAdministratorToken` | 0 (Default) = Disabled<br>1 = Enabled |
| Allow UIAccess applications to prompt for elevation without using the secure desktop | `EnableUIADesktopToggle` | 0 (Default) = Disabled<br>1 = Enabled |
| Behavior of the elevation prompt for administrators in Admin Approval Mode| `ConsentPromptBehaviorAdmin` | 0 = Elevate without prompting<br>1 = Prompt for credentials on the secure desktop<br>2 = Prompt for consent on the secure desktop<br>3 = Prompt for credentials<br>4 = Prompt for consent<br>5 (Default) = Prompt for consent for non-Windows binaries|
| Behavior of the elevation prompt for standard users | `ConsentPromptBehaviorUser` | 0 = Automatically deny elevation requests<br>1 = Prompt for credentials on the secure desktop<br>3 (Default) = Prompt for credentials |
| Detect application installations and prompt for elevation | `EnableInstallerDetection` | 1 = Enabled (default for home only)<br>0 = Disabled (default) |
| Only elevate executables that are signed and validated | `ValidateAdminCodeSignatures` | 0 (Default) = Disabled<br>1 = Enabled |
| Only elevate UIAccess applications that are installed in secure locations | `EnableSecureUIAPaths` | 0 = Disabled<br>1 (Default) = Enabled |
| Run all administrators in Admin Approval Mode | `EnableLUA` | 0 = Disabled<br>1 (Default) = Enabled |
| Switch to the secure desktop when prompting for elevation| `PromptOnSecureDesktop` | 0 = Disabled<br>1 (Default) = Enabled |
| Virtualize file and registry write failures to per-user locations | `EnableVirtualization` | 0 = Disabled<br>1 (Default) = Enabled |
| Prioritise network logons over cached logons | `InteractiveLogonFirst` | 0 (Default) = Disabled<br>1 = Enabled |

[WIN-1]: /windows/client-management/mdm/policy-csp-localpoliciessecurityoptions
[MEM-1]: /mem/intune/configuration/custom-settings-windows-10
[MEM-2]: /mem/intune/configuration/settings-catalog
