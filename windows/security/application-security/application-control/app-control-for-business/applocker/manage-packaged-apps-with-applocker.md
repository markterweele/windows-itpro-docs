---
title: Manage packaged apps with AppLocker
description: Learn concepts and lists procedures to help you manage packaged apps with AppLocker as part of your overall application control strategy.
ms.localizationpriority: medium
ms.topic: how-to
ms.date: 09/11/2024
---

# Manage packaged apps with AppLocker

This article for IT professionals describes concepts and lists procedures to help you manage Packaged apps with AppLocker as part of your overall application control strategy.

## Understanding Packaged apps and Packaged app installers for AppLocker

Packaged apps are based on a model that ensures all the files within an app package share the same identity. With classic Windows apps, each file within the app could have a unique identity. With packaged apps, it's possible to control the entire app by using a single AppLocker rule.

> [!NOTE]
> AppLocker supports only publisher rules for packaged apps. All packaged apps must be signed by the software publisher because Windows does not support unsigned packaged apps.

Typically, an app consists of multiple components: the installer that is used to install the app, and one or more exes, dlls, or scripts. With classic Windows apps, not all these components always share common attributes such as the software's publisher name, product name, and product version. Therefore, AppLocker controls each of these components separately through different rule collections, such as exe, dll, script, and Windows Installer rules. In contrast, all the components of a packaged app share the same publisher name, package name, and package version attributes. Therefore, you can control an entire app with a single rule.

### Comparing classic Windows apps and packaged apps

The rules for classic Windows apps and packaged apps can be enforced in tandem. The differences between packaged apps and classic Windows apps that you should consider include:

- **Installing the apps** - All packaged apps can be installed by a standard user, whereas many classic Windows apps require administrative privileges to install. In an environment where most of the users are standard users, you might need fewer exe rules (because classic Windows apps require administrative privileges to install), but you might need more rules for packaged apps.
- **Changing the system state** - Classic Windows apps can be written to change the system state if they're run with administrative privileges. Most packaged apps can't change the system state because they run with limited privileges. When you design your AppLocker policies, it's important to understand whether an app that you're allowing can make system-wide changes.

AppLocker uses different rule collections to control packaged apps and classic Windows apps. You have the choice to control one type, the other type, or both.

For info about controlling classic Windows apps, see [Administer AppLocker](administer-applocker.md).

For more info about packaged apps, see [Packaged apps and packaged app installer rules in AppLocker](packaged-apps-and-packaged-app-installer-rules-in-applocker.md).

## Design and deployment decisions

You can use two methods to create an inventory of packaged apps on a computer: the AppLocker console or the **Get-AppxPackage** Windows PowerShell cmdlet.

> [!NOTE]
> Not all packaged apps are listed in AppLocker's application inventory wizard. Certain app packages are framework packages that are leveraged by other apps. By themselves, these packages cannot do anything, but blocking such packages can inadvertently cause failure for apps that you want to allow. Instead, you can create Allow or Deny rules for the packaged apps that use these framework packages. The AppLocker user interface deliberately filters out all the packages that are registered as framework packages. For info about how to create an inventory list, see [Create list of apps deployed to each business group](create-list-of-applications-deployed-to-each-business-group.md).

For info about how to use the **Get-AppxPackage** Windows PowerShell cmdlet, see the [AppLocker PowerShell Command Reference](/powershell/module/applocker/).

For info about creating rules for Packaged apps, see [Create a rule for packaged apps](create-a-rule-for-packaged-apps.md).

Consider the following info when you're designing and deploying apps:

- Because AppLocker supports only publisher rules for packaged apps, collecting the installation path information for packaged apps isn't necessary.
- You don't need to create hash- or path-based rules for packaged apps because the software publisher must sign all packaged apps and packaged app installers. Classic Windows apps weren't always consistently signed; therefore, AppLocker has to support hash- or path-based rules.
- By default, if there are no rules in a particular rule collection, AppLocker allows every file that is included in that rule collection. For example, if there are no Windows Installer rules, AppLocker allows all .msi, .msp, and .mst files to run.

> [!NOTE]
> By default AppLocker blocks all packaged apps if the existing domain policy has rules configured in the exe rule collection. You must take explicit action to allow packaged apps in your enterprise. You can allow only a select set of packaged apps. Or if you want to allow all packaged apps, you can create a default rule for the packaged apps collection.

## Using AppLocker to manage packaged apps

Just as there are differences in managing each rule collection, you need to manage the packaged apps with the following strategy:

1. Gather information about which Packaged apps are running in your environment. For information about how to gather this information, see [Create list of apps deployed to each business group](create-list-of-applications-deployed-to-each-business-group.md).

2. Create AppLocker rules for specific packaged apps based on your policy strategies. For more information, see [Create a rule for packaged apps](create-a-rule-for-packaged-apps.md) and [Understanding AppLocker default rules](understanding-applocker-default-rules.md).

3. Continue to update the AppLocker policies as new package apps are introduced into your environment. To do this update, see [Add rules for packaged apps to existing AppLocker rule-set](add-rules-for-packaged-apps-to-existing-applocker-rule-set.md).

4. Continue to monitor your environment to verify the effectiveness of the rules that are deployed in AppLocker policies. To do this monitoring, see [Monitor app usage with AppLocker](monitor-application-usage-with-applocker.md).
