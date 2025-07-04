---
title: Deploy AppLocker policies by using the enforce rules setting
description: This article for IT professionals describes the steps to deploy AppLocker policies by using the enforcement setting method.
ms.localizationpriority: medium
ms.topic: install-set-up-deploy
ms.date: 09/11/2024
---

# Deploy AppLocker policies by using the enforce rules setting

This article for IT professionals describes the steps to deploy AppLocker policies by using the enforcement setting method.

## Background and prerequisites

These procedures assume that your AppLocker policies are deployed with the enforcement mode set to **Audit only**, and you have been collecting data through the AppLocker event logs and other channels to determine what effect these policies have on your environment and the policy's adherence to your application control design.

For info about the AppLocker policy enforcement setting, see [Understand AppLocker enforcement settings](working-with-applocker-rules.md#enforcement-modes).

For info about how to plan an AppLocker policy deployment, see [AppLocker Design Guide](applocker-policies-design-guide.md).

## Step 1: Retrieve the AppLocker policy

Updating an AppLocker policy that is currently enforced in your production environment can cause unintended results. Using Group Policy, you can export the policy from the Group Policy Object (GPO) and then update the rule or rules by using AppLocker on a reference or test PC. For the procedure to do these tasks, see [Export an AppLocker policy from a GPO](export-an-applocker-policy-from-a-gpo.md) and [Import an AppLocker policy into a GPO](import-an-applocker-policy-into-a-gpo.md). For local AppLocker policies, you can update the rule or rules by using the Local Security policy snap-in (secpol.msc) on your AppLocker reference or test PC. For the procedures to do this task, see [Export an AppLocker policy to an XML file](export-an-applocker-policy-to-an-xml-file.md) and [Import an AppLocker policy from another computer](import-an-applocker-policy-from-another-computer.md).

## Step 2: Alter the enforcement setting

Rule enforcement is applied to all rules within a rule collection, not to individual rules. AppLocker divides the rules into collections: executable files, Windows Installer files, packaged apps, scripts, and DLL files. For information about the enforcement mode setting, see [Understand AppLocker Enforcement Settings](working-with-applocker-rules.md#enforcement-modes). For the procedure to alter the enforcement mode setting, see [Configure an AppLocker policy for audit only](configure-an-applocker-policy-for-audit-only.md).

## Step 3: Update the policy

You can edit an AppLocker policy by adding, changing, or removing rules. However, you can't specify a version for the AppLocker policy by importing more rules. To ensure version control when modifying an AppLocker policy, use Group Policy management software that allows you to create versions of GPOs. An example of this type of software is the [Advanced Group Policy Management](/microsoft-desktop-optimization-pack/agpm/) feature from the Microsoft Desktop Optimization Pack.

> [!CAUTION]
> You should not edit an AppLocker rule collection while it is being enforced in Group Policy. Because AppLocker controls what files are allowed to run, making changes to a live policy can cause unexpected behavior.

For the procedure to update the GPO, see [Import an AppLocker policy into a GPO](import-an-applocker-policy-into-a-gpo.md).

For the procedures to distribute policies for local PCs by using the Local Security Policy snap-in (secpol.msc), see [Export an AppLocker policy to an XML file](export-an-applocker-policy-to-an-xml-file.md) and [Import an AppLocker policy from another computer](import-an-applocker-policy-from-another-computer.md).

## Step 4: Monitor the effect of the policy

When a policy is deployed, it's important to monitor the actual implementation of that policy by monitoring your support organization's app access request activity and reviewing the AppLocker event logs. To monitor the effect of the policy, see [Monitor Application Usage with AppLocker](monitor-application-usage-with-applocker.md).

## Other resources

- For steps to perform other AppLocker policy tasks, see [Administer AppLocker](administer-applocker.md).
