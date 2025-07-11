---
title: Document your app list
description: This planning article describes the app information that you should document when you create a list of apps for AppLocker policies.
ms.localizationpriority: medium
ms.topic: article
ms.date: 09/11/2024
---

# Document your app list

This planning article describes the app information that you should document when you create a list of apps for AppLocker policies.

## Record your findings

### Apps

Record the name of the app, its publisher information (if digitally signed), and its importance to the business.

### Installation path

Record the installation path of the apps. For example, Microsoft Office 2016 installs files to *%programfiles%\\Microsoft Office\\Office16\\*, which is *C:\\Program Files\\Microsoft Office\\Office16\\* on most devices.

The following table provides an example of how to list applications for each business group at the early stage of designing your application control policies. Eventually, as more planning information is added to the list, the information can be used to build AppLocker rules.

|Business group|Organizational unit|Implement AppLocker?|Apps|Installation path|
|--- |--- |--- |--- |--- |
|Bank Tellers|Teller-East and Teller-West|Yes|Teller Software|C:\Program Files\Woodgrove\Teller.exe|
||||Windows files|C:\Windows|
|Human Resources|HR-All|Yes|Check Payout|C:\Program Files\Woodgrove\HR\Checkcut.exe|
||||Time Sheet Organizer|C:\Program Files\Woodgrove\HR\Timesheet.exe|
||||Internet Explorer 7|C:\Program Files\Internet Explorer</p>|
||||Windows files|C:\Windows|

>[!NOTE]
>AppLocker only supports publisher rules for Packaged apps. Therefore, collecting the installation path information for Packaged apps is not necessary.

## Event processing

As you create your list of apps, you need to consider how to manage the events generated by user access. The following list is an example of what to consider and what to record:

- Do you want to forward AppLocker events for analysis?
- What is the location of the AppLocker event collection?
- Should an event archival policy be implemented?
- Who analyzes the AppLocker events and how often?
- Should a security policy be in place for event collection?

## Policy maintenance

As you create your list of apps, you need to consider how to manage and maintain the policies that you create. The following list is an example of what to consider and what to record:

- How are rules updated for emergency app access and permanent access?
- How are apps removed?
- How many older versions of the same app are maintained?
- How are new apps introduced?

## Next steps

After you create the list of applications, the next step is to identify the rule collections, which will become the application control policies. This information can be added to the table under the following columns:

- Use default rule or define new rule condition
- Allow or deny
- GPO name

To identify the rule collections, see the following articles:

- [Select the types of rules to create](select-types-of-rules-to-create.md)
- [Determine Group Policy structure and rule enforcement](determine-group-policy-structure-and-rule-enforcement.md)
