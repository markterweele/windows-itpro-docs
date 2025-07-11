---
title: Understand App Control for Business policy design decisions
description: Understand App Control for Business policy design decisions.
ms.localizationpriority: medium
ms.date: 09/11/2024
ms.topic: concept-article
---

# Understand App Control for Business policy design decisions

[!INCLUDE [Feature availability note](../includes/feature-availability-note.md)]

This article is for the IT professional. It lists the design questions, possible answers, and ramifications for decisions made, when planning App Control policies deployment using App Control for Business, within a Windows operating system environment.

When you begin the design and planning process, you should consider the ramifications of your design choices. The resulting decisions will affect your policy deployment scheme and subsequent App Control policy maintenance.

You should consider using App Control for Business as part of your organization's App Control policies if the following are true:

-   You have deployed or plan to deploy the supported versions of Windows in your organization.
-   You need improved control over the access to your organization's applications and the data your users access.
-   Your organization has a well-defined process for application management and deployment.
-   You have resources to test policies against the organization's requirements.
-   You have resources to involve Help Desk or to build a self-help process for end-user application access issues.
-   The group's requirements for productivity, manageability, and security can be controlled by restrictive policies.

## Decide what policies to create

Beginning with Windows 10, version 1903, App Control for Business allows [multiple simultaneous policies](deploy-multiple-appcontrol-policies.md) to be applied to each device. This concurrent application opens up many new use cases for organizations, but your policy management can easily become unwieldy without a well-thought-out plan for the number and types of policies to create.

The first step is to define the desired "circle-of-trust" for your App Control policies. By "circle-of-trust," we mean a description of the business intent of the policy expressed in natural language. This "circle-of-trust" definition will guide you as you create the actual policy rules for your policy XML.

For example, the DefaultWindows policy, which can be found under %OSDrive%\Windows\schemas\CodeIntegrity\ExamplePolicies, establishes a "circle-of-trust" that allows Windows, 3rd-party hardware and software kernel drivers, and applications from the Microsoft Store.

Configuration Manager uses the DefaultWindows policy as the basis for its policy but then modifies the policy rules to allow Configuration Manager and its dependencies, sets the managed installer policy rule, and additionally configures Configuration Manager as a managed installer. It also can optionally authorize apps with positive reputation and perform a one-time scan of folder paths specified by the Configuration Manager administrator, which adds rules for any apps found in the specified paths on the managed endpoint. This process establishes the "circle-of-trust" for Configuration Manager's native App Control integration.

The following questions can help you plan your App Control for Business deployment and determine the right "circle-of-trust" for your policies. They aren't in priority or sequential order, and aren't meant to be an exhaustive set of design considerations.

## App Control design considerations

### How are apps managed and deployed in your organization?

Organizations with well-defined, centrally managed app management and deployment processes can create more restrictive, more secure policies. Other organizations may be able to deploy App Control for Business with more relaxed rules, or may choose to deploy App Control in audit mode to gain better visibility to the apps being used in their organization.

| Possible answers | Design considerations|
| - | - |
| All apps are centrally managed and deployed using endpoint management tools like [Microsoft Intune](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager). | Organizations that centrally manage all apps are best-suited for App Control. App Control for Business options like [managed installer](configure-authorized-apps-deployed-with-a-managed-installer.md) can make it easy to authorize apps that are deployed by the organization's app distribution management solution. |
| Some apps are centrally managed and deployed, but teams can install other apps for their members. | [Supplemental policies](deploy-multiple-appcontrol-policies.md) can be used to allow team-specific exceptions to your core organization-wide App Control for Business policy. Alternatively, teams can use managed installers to install their team-specific apps, or admin-only file path rules can be used to allow apps installed by admin users. |
| Users and teams are free to download and install apps but the organization wants to restrict that right to prevalent and reputable apps only. | App Control for Business can integrate with Microsoft's [Intelligent Security Graph](use-appcontrol-with-intelligent-security-graph.md) (the same source of intelligence that powers Microsoft Defender Antivirus and Windows Defender SmartScreen) to allow only apps and binaries that have positive reputation. |
| Users and teams are free to download and install apps without restriction. | App Control for Business policies can be deployed in audit mode to gain insight into the apps and binaries running in your organization without impacting user and team productivity.|

### Are internally developed line-of-business (LOB) apps and apps developed by third-party companies digitally signed?

Traditional Win32 apps on Windows can run without being digitally signed. This practice can expose Windows devices to malicious or tampered code and presents a security vulnerability to your Windows devices. Adopting code-signing as part of your organization's app development practices or augmenting apps with signed catalog files as part of your app ingestion and distribution can greatly improve the integrity and security of apps used.

| Possible answers | Design considerations |
| - | - |
| All apps used in your organization must be signed. | Organizations that enforce [codesigning](../deployment/use-code-signing-for-better-control-and-protection.md) for all executable code are best-positioned to protect their Windows computers from malicious code execution. App Control for Business rules can be created to authorize apps and binaries from the organization's internal development teams and from trusted independent software vendors (ISV). |
| Apps used in your organization don't need to meet any codesigning requirements. | Organizations can  [use built-in Windows tools](../deployment/deploy-catalog-files-to-support-appcontrol.md) to add organization-specific App Catalog signatures to existing apps as a part of the app deployment process, which can be used to authorize code execution. Solutions like Microsoft Intune offer multiple ways to distribute signed App Catalogs. |

### Are there specific groups in your organization that need customized App Control policies?

Most business teams or departments have specific security requirements that pertain to data access and the applications used to access that data. Consider the scope of the project for each group and the group's priorities before you deploy App Control policies for the entire organization. There's overhead in managing policies that might lead you to choose between broad, organization-wide policies and multiple team-specific policies.

| Possible answers | Design considerations |
| - | - |
| Yes | App Control policies can be created unique per team, or team-specific supplemental policies can be used to expand what is allowed by a common, centrally defined base policy.|
| No | App Control policies can be applied globally to applications that are installed on PCs running Windows 10 and Windows 11. Depending on the number of apps you need to control, managing all the rules and exceptions might be challenging.|

### Does your IT department have resources to analyze application usage, and to design and manage the policies?

The time and resources that are available to you to perform the research and analysis can affect the detail of your plan and processes for continuing policy management and maintenance.

| Possible answers | Design considerations |
| - | - |
| Yes | Invest the time to analyze your organization's App Control requirements, and plan a complete deployment that uses rules that are constructed as possible.|
| No | Consider a focused and phased deployment for specific groups by using few rules. As you apply controls to applications in a specific group, learn from that deployment to plan your next deployment. Alternatively, you can create a policy with a broad trust profile to authorize as many apps as possible. |

### Does your organization have Help Desk support?

Preventing your users from accessing known, deployed, or personal applications will initially cause an increase in end-user support. It will be necessary to address the various support issues in your organization so security policies are followed and business workflow isn't hampered.

| Possible answers | Design considerations |
| - | - |
| Yes | Involve the support department early in the planning phase because your users may inadvertently be blocked from using their applications, or they may seek exceptions to use specific applications. |
| No | Invest time in developing online support processes and documentation before deployment. |
