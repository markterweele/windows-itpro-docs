---
title: Microsoft Security Compliance Toolkit Guide
description: This article describes how to use Security Compliance Toolkit in your organization.
ms.topic: concept-article
ms.date: 10/01/2024
---

# Microsoft Security Compliance Toolkit - How to use

## What is the Security Compliance Toolkit (SCT)?

The Security Compliance Toolkit (SCT) is a set of tools that allows enterprise security administrators to download, analyze, test, edit, and store Microsoft-recommended security configuration baselines for Windows and other Microsoft products.

The SCT enables administrators to effectively manage their enterprise's Group Policy Objects (GPOs). Using the toolkit, administrators can compare their current GPOs with Microsoft-recommended GPO baselines or other baselines, edit them, store them in GPO backup file format, and apply them broadly through Active Directory or individually through local policy.

The Security Compliance Toolkit consists of:

- Windows 11 security baseline
  - Windows 11, version 24H2
  - Windows 11, version 23H2
  - Windows 11, version 22H2
  - Windows 11, version 21H2
- Windows 10 security baselines
  - Windows 10, version 22H2
  - Windows 10, version 21H2
  - Windows 10, version 1809
  - Windows 10, version 1607
  - Windows 10, version 1507
- Windows Server security baselines
  - Windows Server 2025
  - Windows Server 2022
  - Windows Server 2019
  - Windows Server 2016
- Microsoft Office security baseline
  - Microsoft 365 Apps for Enterprise Version 2412
- Microsoft Edge security baseline
  - Microsoft Edge version 128
- Tools
  - Policy Analyzer
  - Local Group Policy Object (LGPO)
  - Set Object Security
  - GPO to Policy Rules

You can [download the tools](https://www.microsoft.com/download/details.aspx?id=55319) along with the baselines for the relevant Windows versions. For more information about security baseline recommendations, see the [Microsoft Security Guidance blog](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/bg-p/Microsoft-Security-Baselines).

## What is the Policy Analyzer tool?

The Policy Analyzer is a utility for analyzing and comparing sets of Group Policy Objects (GPOs). Its main features include:

- Highlight when a set of Group Policies has redundant settings or internal inconsistencies
- Highlight the differences between versions or sets of Group Policies
- Compare GPOs against current local policy and local registry settings
- Export results to a Microsoft Excel spreadsheet

Policy Analyzer lets you treat a set of GPOs as a single unit. This treatment makes it easy to determine whether particular settings are duplicated across the GPOs or are set to conflicting values. Policy Analyzer also lets you capture a baseline and then compare it to a snapshot taken at a later time to identify changes anywhere across the set.

More information on the Policy Analyzer tool can be found on the [Microsoft Security Guidance blog](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/new-amp-updated-security-tools/ba-p/1631613) or by [downloading the tool](https://www.microsoft.com/download/details.aspx?id=55319).

## What is the Local Group Policy Object (LGPO) tool?

`LGPO.exe` is a command-line utility that is designed to help automate management of Local Group Policy. Using local policy gives administrators a simple way to verify the effects of Group Policy settings, and is also useful for managing non-domain-joined systems. `LGPO.exe` can import and apply settings from Registry Policy (Registry.pol) files, security templates, Advanced Auditing backup files, and from formatted "LGPO text" files. It can export local policy to a GPO backup. It can export the contents of a Registry Policy file to the "LGPO text" format that can then be edited, and can build a Registry Policy file from an LGPO text file.

Documentation for the LGPO tool can be found on the [Microsoft Security Guidance blog](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/new-amp-updated-security-tools/ba-p/1631613) or by [downloading the tool](https://www.microsoft.com/download/details.aspx?id=55319).

## What is the Set Object Security tool?

`SetObjectSecurity.exe` enables you to set the security descriptor for just about any type of Windows securable object, such as files, directories, registry keys, event logs, services, and SMB shares. For file system and registry objects, you can choose whether to apply inheritance rules. You can also choose to output the security descriptor in a `.reg` file compatible representation of the security descriptor for a REG_BINARY registry value.

Documentation for the Set Object Security tool can be found on the [Microsoft Security Baselines blog](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/new-amp-updated-security-tools/ba-p/1631613) or by [downloading the tool](https://www.microsoft.com/download/details.aspx?id=55319).

## What is the GPO to Policy Rules tool?

Automate the conversion of GPO backups to Policy Analyzer `.PolicyRules` files and skip the GUI. GPO2PolicyRules is a command-line tool that is included with the Policy Analyzer download.

Documentation for the GPO to PolicyRules tool can be found on the [Microsoft Security Baselines blog](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/new-amp-updated-security-tools/ba-p/1631613) or by [downloading the tool](https://www.microsoft.com/download/details.aspx?id=55319).
