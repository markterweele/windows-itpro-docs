---
title: Application Control for Windows
description: Application Control restricts which applications users are allowed to run and the code that runs in the system core.
ms.localizationpriority: medium
ms.collection:
- tier3
ms.date: 01/28/2025
ms.topic: overview
---

# Application Control for Windows

[!INCLUDE [Feature availability note](includes/feature-availability-note.md)]

Your organization's data is one of its most valuable assets... and adversaries want it. No matter what security controls you apply over your data, they are only as strong as the weakest link: the trusted user sitting at the keyboard. When a user runs a process, that process shares the same access to your data that the user has. So your sensitive information is easily transmitted, modified, deleted or encrypted when a user, knowingly or unknowingly, runs malicious software. And with thousands of new malicious files created every day, relying solely on traditional methods like antivirus (AV) solutions gives you an inadequate defense against new attacks. Application control is a crucial line of defense against today's threat actors. 

Application control works alongside your AV solution to help mitigate these types of security threats by restricting the apps that users can run and even what code runs in the System Core (kernel). Application control policies can also block unsigned scripts and MSIs, and restrict Windows PowerShell to run in [Constrained Language Mode](/powershell/module/microsoft.powershell.core/about/about_language_modes).

It moves you from a trust model where all code runs unless your AV solution confidently predicts it's bad, to one where apps run only if your policy says so. Government and security organizations, like the Australian Signals Directorate, frequently cite application control as one of the most effective ways to address the threat of executable file-based malware (.exe, .dll, etc.).

> [!NOTE]
> Although application control can significantly harden your computers against malicious code, it's not a replacement for antivirus. You should continue to maintain your active antivirus solution alongside App Control for a well-rounded enterprise security portfolio.

Windows 10 and Windows 11 include two application control technologies that your organization can use depending on your specific scenarios and requirements:

- **App Control for Business (app control)**; and
- **AppLocker**

## App Control and Smart App Control

Starting in Windows 11 version 22H2, [Smart App Control](https://support.microsoft.com/topic/what-is-smart-app-control-285ea03d-fa88-4d56-882e-6698afdb7003) brings robust application control to consumers and to some small businesses with simpler app portfolios. Smart App Control ensures only signed code runs as well as code predicted to be safe by our intelligent cloud-powered security service. When code is unsigned and the service is unable to predict with confidence that it is safe to run, it is blocked but can develop better reputation over time as new signals are processed by the service. Meanwhile, code determined to be unsafe is always blocked.

While Smart App Control is designed for consumers, we believe it's the ideal starting point for most organizations. And since it's built entirely upon App Control for Business, you can create a policy with the same security and compatibility as Smart App Control but which also trusts the line-of-business (LOB) apps that your organization depends on. The service providing Smart App Control's intelligence to predict what code is safe to run is also available in App Control for Business, where it's called the Intelligent Security Graph (ISG).

Smart App Control starts in evaluation mode and will switch itself off within 48 hours for enterprise managed devices unless the user has turned it on first. If you want to proactively turn off Smart App Control across your organization's endpoints, set the **VerifiedAndReputablePolicyState** (DWORD) registry value under `HKLM\SYSTEM\CurrentControlSet\Control\CI\Policy` as shown in the following table. After you change the registry value, you must run [CiTool.exe -r](operations/citool-commands.md#refresh-the-app-control-policies-on-the-system) for the change to take effect.

| Value | Description |
|-------|-------------|
| 0     | Off         |
| 1     | Enforce     |
| 2     | Evaluation  |

> [!IMPORTANT]
> Once you turn Smart App Control off, it can't be turned on without resetting or reinstalling Windows.

The App Control policy used for Smart App Control comes bundled with the [App Control Wizard](design/appcontrol-wizard.md) policy authoring tool and is also found as an [example policy](design/example-appcontrol-base-policies.md) at *%windir%/schemas/CodeIntegrity/ExamplePolicies/SmartAppControl.xml*. To use this example policy as a starting point for your own policy, see [Create a custom base policy using an example App Control base policy](design/create-appcontrol-policy-for-lightly-managed-devices.md#create-a-custom-base-policy-using-an-example-app-control-base-policy). When using the Smart App Control example policy as the basis for your own custom policy, you must remove the option **Enabled:Conditional Windows Lockdown Policy** so it is ready for use as an App Control for Business policy.

[!INCLUDE [windows-defender-application-control-wdac](../../../../../includes/licensing/windows-defender-application-control-wdac.md)]

## What you should read next

Read on to learn more about the two application control technologies available in Windows with the [App Control for Business and AppLocker Overview](./appcontrol-and-applocker-overview.md).

If you're ready to jump in and get started creating policies, let's revisit Smart App Control and [Use the Smart App Control policy to build your own starter policy](design/create-appcontrol-policy-for-lightly-managed-devices.md).
