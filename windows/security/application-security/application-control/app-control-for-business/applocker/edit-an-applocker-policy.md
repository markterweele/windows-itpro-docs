---
title: Edit an AppLocker policy
description: This article for IT professionals describes the steps required to modify an AppLocker policy.
ms.localizationpriority: medium
ms.topic: how-to
ms.date: 09/11/2024
---

# Edit an AppLocker policy

This article for IT professionals describes the steps required to modify an AppLocker policy.

You can edit an AppLocker policy by adding, changing, or removing rules. However, you can't create a new version of the policy by importing more rules. To modify an AppLocker policy that is in production, you should use Group Policy management software that allows you to version Group Policy Objects (GPOs). If you want to merge multiple AppLocker policies into a single one, you can either manually merge the policies or use the Windows PowerShell cmdlets for AppLocker. You can't automatically merge policies by using the AppLocker snap-in. You must create one rule collection from two or more policies. The AppLocker policy is saved in XML format, and the exported policy can be edited with any text or XML editor. For info about merging policies, see [Merge AppLocker policies manually](merge-applocker-policies-manually.md) or [Merge AppLocker policies by using Set-ApplockerPolicy](merge-applocker-policies-by-using-set-applockerpolicy.md).

There are three methods you can use to edit an AppLocker policy:

- [Editing an AppLocker policy by using Mobile Device Management (MDM)](#editing-an-applocker-policy-by-using-mobile-device-management-mdm)
- [Editing an AppLocker policy by using Group Policy](#editing-an-applocker-policy-by-using-group-policy)
- [Editing an AppLocker policy by using the Local Security Policy snap-in](#editing-an-applocker-policy-by-using-the-local-security-policy-snap-in)

## Editing an AppLocker policy by using Mobile Device Management (MDM)

To edit an AppLocker policy deployed using the AppLocker configuration service provider (CSP), update the content in the string value of the CSP's policy node.

For more information, see the [AppLocker CSP](/windows/client-management/mdm/applocker-csp).

## Editing an AppLocker policy by using Group Policy

The steps to edit an AppLocker policy distributed by Group Policy include:

### Step 1: Use Group Policy management software to export the AppLocker policy from the GPO

AppLocker provides a feature to export and import AppLocker policies as an XML file. This feature allows you to modify an AppLocker policy outside your production environment. Because updating an AppLocker policy in a deployed GPO could have unintended consequences, you should first export the AppLocker policy to an XML file. For information on the procedure to export this policy, see [Export an AppLocker policy from a GPO](export-an-applocker-policy-from-a-gpo.md).

### Step 2: Import the AppLocker policy into the AppLocker reference PC or the PC you use for policy maintenance

After exporting the AppLocker policy to an XML file, you should import the XML file onto a reference PC so that you can edit the policy. For information on the procedure to import an AppLocker policy, see [Import an AppLocker policy from another computer](import-an-applocker-policy-from-another-computer.md).

> [!IMPORTANT]
> Importing a policy onto another PC will overwrite the existing policy on that PC.

### Step 3: Use AppLocker to modify and test the rule

AppLocker provides ways to modify, delete, or add rules to a policy by modifying the rules within the collection.

- For information on the procedure to modify a rule, see [Edit AppLocker rules](edit-applocker-rules.md).
- For information on the procedure to delete a rule, see [Delete an AppLocker rule](delete-an-applocker-rule.md).
- For procedures to create rules, see:
  - [Create a rule that uses a publisher condition](create-a-rule-that-uses-a-publisher-condition.md)
  - [Create a rule that uses a path condition](create-a-rule-that-uses-a-path-condition.md)
  - [Create a rule that uses a file hash condition](create-a-rule-that-uses-a-file-hash-condition.md)
  - [Enable the DLL rule collection](enable-the-dll-rule-collection.md)
- For information on the steps to test an AppLocker policy, see [Test and update an AppLocker policy](test-and-update-an-applocker-policy.md).
- For procedures to export the updated policy from the reference computer back into the GPO, see [Export an AppLocker policy to an XML file](export-an-applocker-policy-to-an-xml-file.md) and [Import an AppLocker policy into a GPO](import-an-applocker-policy-into-a-gpo.md).

### Step 4: Use AppLocker and Group Policy to import the AppLocker policy back into the GPO

For procedures to export the updated policy from the reference computer back into the GPO, see [Export an AppLocker policy to an XML file](export-an-applocker-policy-to-an-xml-file.md) and [Import an AppLocker policy into a GPO](import-an-applocker-policy-into-a-gpo.md).

> [!IMPORTANT]
> You should avoid editing an AppLocker rule collection while it is being enforced in Group Policy. Because AppLocker controls what files are allowed to run, making changes to a live policy can cause unexpected behavior. For info about testing policies, see [Test and update an AppLocker policy](test-and-update-an-applocker-policy.md).

> [!NOTE]
> If you are performing these steps by using Microsoft Advanced Group Policy Management (AGPM), check out the GPO before exporting the policy.

## Editing an AppLocker policy by using the Local Security Policy snap-in

The steps to edit an AppLocker policy distributed by using the Local Security Policy snap-in (secpol.msc) include the following tasks.

### Step 1: Import the AppLocker policy

On the PC where you maintain policies, open the AppLocker snap-in from the Local Security Policy snap-in (secpol.msc). If you exported the AppLocker policy from another PC, use AppLocker to import it onto the PC.

After exporting the AppLocker policy to an XML file, you should import the XML file onto a reference PC so that you can edit the policy. For information on the procedure to import an AppLocker policy, see [Import an AppLocker policy from another computer](import-an-applocker-policy-from-another-computer.md).

> [!IMPORTANT]
> Importing a policy onto another PC will overwrite the existing policy on that PC.

### Step 2: Identify and modify the rule to change, delete, or add

AppLocker provides ways to modify, delete, or add rules to a policy by modifying the rules within the collection.

- For information on the procedure to modify a rule, see [Edit AppLocker rules](edit-applocker-rules.md).
- For information on the procedure to delete a rule, see [Delete an AppLocker rule](delete-an-applocker-rule.md).
- For procedures to create rules, see:
  - [Create a rule that uses a publisher condition](create-a-rule-that-uses-a-publisher-condition.md)
  - [Create a rule that uses a path condition](create-a-rule-that-uses-a-path-condition.md)
  - [Create a rule that uses a file hash condition](create-a-rule-that-uses-a-file-hash-condition.md)
  - [Enable the DLL rule collection](enable-the-dll-rule-collection.md)

### Step 3: Test the effect of the policy

For steps to test an AppLocker policy, see [Test and update an AppLocker policy](test-and-update-an-applocker-policy.md).

### Step 4: Export the policy to an XML file and propagate it to all targeted computers

For procedures to export the updated policy from the reference computer to targeted computers, see [Export an AppLocker policy to an XML file](export-an-applocker-policy-to-an-xml-file.md) and [Import an AppLocker policy from another computer](import-an-applocker-policy-from-another-computer.md).

## Other resources

- For steps to perform other AppLocker policy tasks, see [Administer AppLocker](administer-applocker.md).
