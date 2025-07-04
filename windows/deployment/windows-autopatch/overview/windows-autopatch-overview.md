---
title: What is Windows Autopatch?
description: Details what the service is and shortcuts to articles.
ms.date: 03/31/2025
ms.service: windows-client
ms.subservice: autopatch
ms.topic: overview
ms.localizationpriority: medium
author: tiaraquan
ms.author: tiaraquan
manager: bpardi
ms.collection:
  - highpri
  - tier1
ms.reviewer: hathind
---

# What is Windows Autopatch?

> [!IMPORTANT]
> In April 2025, Windows Autopatch removed feature activation and made Windows Autopatch features available to Business Premium and A3+ licenses. These changes are rolling out over the next several weeks. If your experience looks different from the documentation, you didn’t receive the changes yet. Review [Prerequisites](../prepare/windows-autopatch-prerequisites.md) and [Features and capabilities](#features-and-capabilities) to understand licensing and feature entitlement.

Windows Autopatch is a cloud service that automates Windows, Microsoft 365 Apps for enterprise, Microsoft Edge, and Microsoft Teams updates to improve security and productivity across your organization.

## Unique to Windows Autopatch

Rather than maintaining complex digital infrastructure, businesses want to focus on what makes them unique and successful. Windows Autopatch offers a solution to some of the challenges facing businesses and their people today:

- **Close the security gap**: Windows Autopatch keeps Microsoft Windows current, there are fewer vulnerabilities and threats to your devices.
- **Close the productivity gap**: Windows Autopatch adopts features as they're made available. End users get the latest tools to amplify their collaboration and work.
- **Optimize your IT admin resources**: Windows Autopatch automates routine endpoint updates. IT pros have more time to create value.
- **On-premises infrastructure**: Transitioning to the world of software as a service (SaaS) allows you to minimize your investment in on-premises hardware since updates are delivered from the cloud.
- **Onboard new services**: Windows Autopatch makes it easy to enroll and minimizes the time required from your IT Admins to get started.
- **Minimize end user disruption**: Windows Autopatch releases updates in sequential deployment rings, and responding to reliability and compatibility signals, user disruptions due to updates are minimized.

Windows Autopatch helps you minimize the involvement of your scarce IT resources in the planning and deployment of updates for Windows, Microsoft 365 Apps, Microsoft Edge, or Teams. Windows Autopatch uses careful rollout sequences and communicates with you throughout the release so that IT Admins can focus on other activities and tasks.

## Features and capabilities

The goal of Windows Autopatch is to deliver software updates to registered devices; the service frees up IT and minimizes disruptions to your end users. Once a device is registered with the service, you have access to the following features through the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431):

### Features included with Business Premium, A3+, E3+ and F3 licenses

| Features included with Business Premium, A3+, E3+ and F3 licenses | Description |
| --- | --- |
| [Role-based access control](../prepare/windows-autopatch-role-based-access-control.md) | Use role-based access control in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to manage who has access to your organization's resources and what they can do with those resources. |
| [Update rings](../manage/windows-autopatch-update-rings.md) | You can manage Update rings for Windows 10 and later devices with Windows Autopatch. For more information, see [Manage Update rings](../manage/windows-autopatch-update-rings.md). |
| [Autopatch groups](../deploy/windows-autopatch-groups-overview.md) | You can manage update deployment based on your audience.<p>An Autopatch group is a logical container or unit that groups several [Microsoft Entra groups](/entra/fundamentals/groups-view-azure-portal), and software update policies, such as [Update rings policy for Windows 10 and later](/mem/intune/protect/windows-10-update-rings) and [feature updates policy for Windows 10 and later policies](/mem/intune/protect/windows-10-feature-updates).</p><p>For more information about workloads supported by Autopatch groups, see [Software update workloads](../deploy/windows-autopatch-groups-overview.md#software-update-workloads).</p> |
| [Windows quality updates](../manage/windows-autopatch-windows-quality-update-overview.md) | With Windows Autopatch, you can manage Windows quality update profiles for Windows 10 and later devices. You can expedite a specific Windows quality update using targeted policies. Windows Autopatch:<ul><li>Aims to keep at least 95% of [Up to Date devices](../monitor/windows-autopatch-windows-quality-and-feature-update-reports-overview.md#up-to-date-devices) on the latest quality update. For more information, see [Windows quality update Service Level Objective](../manage/windows-autopatch-windows-quality-update-overview.md#service-level-objective).</li></ul> |
| [Hotpatch updates](../manage/windows-autopatch-hotpatch-updates.md) | Install [Monthly B release security updates](/windows/deployment/update/release-cycle#monthly-security-update-release) without requiring you to restart the device. |
| [Windows feature updates](../manage/windows-autopatch-windows-feature-update-overview.md) and [Multi-phase release policies with feature updates](../manage/windows-autopatch-windows-feature-update-overview.md#multi-phase-feature-update) | Windows Autopatch provides tools to assist with the controlled roll out of annual Windows feature updates. With multi-phase release policies, you can create customizable feature update deployments using multiple phases for your existing Autopatch groups. These phased releases can be tailored to meet the unique needs of your organization.|
| [Driver and firmware updates](../manage/windows-autopatch-manage-driver-and-firmware-updates.md) | You can manage and control your driver and firmware updates with Windows Autopatch. You can:<ul><li>Choose to receive driver and firmware updates automatically, or self-manage the deployment</li><li>Control the flow of all drivers to an Autopatch group or rings within an Autopatch group</li><li>Control the flow of a specific driver or firmware across your entire tenant via approvals</li><li>Approve and deploy [other drivers and firmware](../manage/windows-autopatch-manage-driver-and-firmware-updates.md#other-drivers-and-firmware) that previously couldn’t be centrally managed</li></ul> |
| [Microsoft 365 Apps for enterprise updates](../manage/windows-autopatch-microsoft-365-apps-enterprise.md) | Windows Autopatch aims to keep at least 90% of eligible devices on a supported version of the Monthly Enterprise Channel (MEC). |
| [Microsoft Edge updates](../manage/windows-autopatch-edge.md) | Windows Autopatch configures eligible devices to benefit from Microsoft Edge's progressive rollouts on the Stable channel. |
| [Microsoft Teams updates](../manage/windows-autopatch-teams.md) | Windows Autopatch allows eligible devices to benefit from the standard automatic update channel. |
| [Intune reports](/intune/intune-service/fundamentals/reports) | Use Intune reports to monitor the health and activity of endpoints in your organization.|
| [Hotpatch quality update report](../monitor/windows-autopatch-hotpatch-quality-update-report.md) | Hotpatch quality update report provides a per policy level view of the current update statuses for all devices that receive Hotpatch updates. |
| Enhanced [Windows quality and feature update reports](../monitor/windows-autopatch-windows-quality-and-feature-update-reports-overview.md) and [device alerts](../monitor/windows-autopatch-device-alerts.md) | Using Windows quality and feature update reports, you can monitor and remediate managed devices that are Not up to Date and resolve any device alerts to bring managed devices back into compliance. |

### Features included with E3+ and F3 licenses only

In addition to the features listed in the previous table, if you have Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5), you have access to the following through the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431):

| Feature included with E3+ and F3 licenses only | Description |
| --- | ---- |
| [Submit support requests](../manage/windows-autopatch-support-request.md) with the Windows Autopatch Service Engineering Team | You can submit, manage, and edit support requests. |

## Communications

To stay informed of upcoming changes, including new and changed features, planned maintenance, release and status communications, or other important announcements, navigate to [Microsoft 365 admin center > Message center](https://admin.microsoft.com/adminportal/home#/MessageCenter).

## Accessibility

Microsoft remains committed to the security of your data and the [accessibility](https://www.microsoft.com/trust-center/compliance/accessibility) of our services. For more information, see the [Microsoft Trust Center](https://www.microsoft.com/trust-center) and the [Office Accessibility Center](https://support.office.com/article/ecab0fcf-d143-4fe8-a2ff-6cd596bddc6d).

## Have feedback or would like to start a discussion?

You can [provide feedback](https://go.microsoft.com/fwlink/?linkid=2195593) or start a discussion in our [Windows Autopatch Tech Community](https://aka.ms/Community/WindowsAutopatch).
