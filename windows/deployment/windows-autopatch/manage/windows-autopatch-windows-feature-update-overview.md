---
title: Windows feature updates overview
description: This article explains how Windows feature updates are managed
ms.date: 05/27/2025
ms.service: windows-client
ms.subservice: autopatch
ms.topic: overview
ms.localizationpriority: medium
author: tiaraquan
ms.author: tiaraquan
manager: bpardi
ms.reviewer: andredm7
ms.collection:
  - highpri
  - tier1
---

# Windows feature update

Windows Autopatch provides tools to assist with the controlled roll out of annual Windows feature updates. These policies provide tools to allow version targeting, phased releases, and even Windows 10 to Windows 11 update options. For more information about how to configure feature update profiles, see [Feature updates for Windows 10 and later policy in Intune](/mem/intune/protect/windows-10-feature-updates).

> [!IMPORTANT]
> Windows Autopatch supports registering [Windows 10 and Windows 11 Long-Term Servicing Channel (LTSC)](/windows/whats-new/ltsc/overview) devices that are being currently serviced by the [Windows 10 LTSC](/windows/release-health/release-information) or [Windows 11 LTSC](/windows/release-health/windows11-release-information). The service only supports managing the [Windows quality updates](../operate/windows-autopatch-windows-quality-update-overview.md) workload for devices currently serviced by the LTSC. Windows Update client policies and Windows Autopatch don't offer Windows feature updates for devices that are part of the LTSC. You must either use [LTSC media](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise) or the [Configuration Manager Operating System Deployment capabilities to perform an in-place upgrade](/windows/deployment/deploy-windows-cm/upgrade-to-windows-10-with-configuration-manager) for Windows devices that are part of the LTSC.

## Multi-phase feature update

With multi-phase feature updates, you can create customizable feature update deployments using multiple phases for your [existing Autopatch groups](../manage/windows-autopatch-manage-autopatch-groups.md). These phased releases can be tailored to meet your organizational unique needs.

### Release statuses

A release is made of one or more phases. The release status is based on the calculation and consolidation of each phase status.

The release statuses are described in the following table:

| Release status | Definition | Options |
| ----- | ----- | ----- |
| Scheduled | Release is scheduled and not all phases created its Windows feature update policies |<ul><li>Releases with the **Scheduled status** can't be canceled but can have its deployment cadence edited as not all phases created its Windows feature update policies.</li><li>Autopatch groups and its deployment rings that belong to a **Scheduled** release can't be assigned to another release.</li></ul> |
| Active | All phases in the release are active. All phases reached their first deployment date, which created the Windows feature update policies. |<ul><li>Release can be paused but can't be edited or canceled since the Windows feature update policy was already created for its phases.</li><li>Autopatch groups and their deployment rings can be assigned to another release.</li></ul> |
| Inactive | All the Autopatch groups within the release are assigned to a new release. As a result, the Windows feature update policies were unassigned from all phases from within the release. |<ul><li>Release can be viewed as a historical record.</li><li>Releases can't be deleted, edited, or canceled.</li></ul> |
| Paused | All phases in the release are paused. The release remains paused until you resume it. | <ul><li>Releases with the Paused status can't be edited or canceled since the Windows feature update policy was already created for its phases.</li><li>Release can be resumed.</li></ul> |
| Canceled | All phases in the release are canceled. | <ul><li>Releases with the Canceled status can't be edited or canceled since the Windows feature update policy wasn't created for its phases.</li><li>Canceled release can't be deleted.</li></ul> |
| Assignment error | The release is scheduled but one or more policies aren't assigned. The user that created the release doesn't have the required permissions to assign one or more policies because the selected Autopatch group isn't in their Scoped Group. Contact the Intune administrator or Role administrator to complete steps in [Scoped admins and Autopatch groups](../prepare/windows-autopatch-role-based-access-control.md#scoped-admins-and-autopatch-groups). |

#### Phase statuses

A phase is made of one or more [Autopatch group deployment rings](../deploy/windows-autopatch-groups-overview.md#autopatch-group-deployment-rings). Each phase reports its status to its release.

> [!IMPORTANT]
> The determining factor that makes a phase status transition from **Scheduled** to **Active** is when the service automatically creates the Windows feature update policy for each Autopatch group deployment ring. Additionally, the phase status transition from **Active** to **Inactive** occurs when Windows feature update policies are unassigned from the Autopatch groups that belong to a phase. This can happen when an Autopatch group and its deployment rings are reused as part of a new release.

| Phase status | Definition |
| ----- | ----- |
| Scheduled | The phase is scheduled but didn't reach its first deployment date yet. The Windows feature update policy wasn't created for the respective phase yet. |
| Active | The first deployment date reached. The Windows feature update policy was created for the respective phase. |
| Inactive | All Autopatch groups within the phase are reassigned to a new release. All Windows feature update policies were unassigned from the Autopatch groups. |
| Paused | Phase is paused. You must resume the phase. |
| Canceled | Phase is canceled. All Autopatch groups within the phase can be used with a new release. A phase that is canceled can't be deleted. |
| Assignment error | The phase is scheduled but the policy isn't assigned. The user that created the policy doesn't have the required permissions to assign the policy because the selected Autopatch group isn't in their Scoped Group. Contact the Intune Administrator or Role administrator to complete steps in [Scoped admins and Autopatch groups](../prepare/windows-autopatch-role-based-access-control.md#scoped-admins-and-autopatch-groups). |

#### Phase policy configuration

Windows Autopatch creates one Windows feature update policy per phase using the following naming convention:

**`Windows Autopatch - DSS policy - <Release Name> - Phase <Phase Number>`**

These policies can be viewed in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

The following table is an example of the Windows feature update policies that were created for phases within a release:

| Policy name | Feature update version | Rollout options| Day between groups | Support end date |
| ----- | ----- | ----- | ----- | ----- |
| Windows Autopatch - DSS Policy - My feature update release - Phase 1  | Windows 10 22H2 | Make update available as soon as possible| N/A | October 14, 2025 |
| Windows Autopatch - DSS Policy - My feature update release - Phase 2  | Windows 10 22H2 | Make update available as soon as possible | 7 | October 14, 2025 |
| Windows Autopatch - DSS Policy - My feature update release - Phase 3  | Windows 10 22H2 | Make update available as soon as possible | 7 | October 14, 2025 |
| Windows Autopatch - DSS Policy - My feature update release - Phase 4  | Windows 10 22H2 | Make update available as soon as possible | 7 | October 14, 2025 |
| Windows Autopatch - DSS Policy - My feature update release - Phase 5  | Windows 10 22H2 | Make update available as soon as possible | 7 | October 14, 2025 |

## Create a custom release

**To create a custom release:**

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** from the left navigation menu.
1. Under the **Manage updates** section, select **Windows updates**.
1. In the **Windows updates** blade, select the **Feature updates** tab.
1. Select **Create Autopatch multi-phase release**.
1. In the **Basics** page:
    1. Enter a **Name** for the custom release.
    2. Select the **Version** to deploy.
    3. Enter a **Description** for the custom release.
    4. Select **Next**.
1. In the **Autopatch groups** page, choose one or more existing Autopatch groups you want to include in the custom release, then select Next.
1. You can't choose Autopatch groups that are already part of an existing custom release. Select **Autopatch groups assigned to other releases** to review existing assignments.
1. In the Release phases page, review the number of autopopulated phases. You can Edit, Delete, and Add a phase based on your needs. Once you're ready, select **Next**. **Before you proceed to the next step**, all deployment rings must be assigned to a phase, and all phases must have deployment rings assigned.
1. In the **Release schedule** page, choose **First deployment date**, and the number of **Gradual rollout groups**, then select **Next**. **You can only select the next day**, not the current day, as the first deployment date. The service creates feature update policy for Windows 10 and later twice a day at 4:00AM and 4:00PM (UTC) and can't guarantee that the release starts on the current day given the UTC variance across the globe.
    1. The **Goal completion date** only applies to the [Deadline-driven deployment cadence type](../operate/windows-autopatch-groups-windows-update.md#deadline-driven). The Deadline-drive deployment cadence type can be specified when you configure the Windows Updates settings during the Autopatch group creation/editing flow.
    2. Additionally, the formula for the goal completion date is `<First Deployment Date> + (<Number of gradual rollout groups> - 1) * Days in between groups (7) + Deadline for feature updates (5 days) + Grace Period (2 days)`.
1. In the **Review + create** page, review all settings. Once you're ready, select **Create**.

> [!NOTE]
> Custom releases can't be deleted from the Feature updates tab in the Windows updates blade. The custom release record serves as a historical record for auditing purposes when needed.

## Edit a custom release

> [!NOTE]
> Only custom releases that have the **Scheduled** status can be edited. A release phase can only be edited prior to reaching its first deployment date. Additionally, you can only edit the deployment dates when editing a release.

**To edit a custom release:**

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** from the left navigation menu.
1. Under the **Manage updates** section, select **Windows updates**.
1. In the **Windows update** blade, select the **Feature updates** tab.
1. In the **Feature updates** tab, select the **horizontal ellipses (…)** > Edit to customize your gradual rollout of your feature updates release, then select **Save**.
    1. Only the release schedule can be customized when using the edit function. You can't add or remove Autopatch groups or modify the phase order when editing a release.
1. Select **Review + Create**.
1. Select **Apply** to save your changes.

## Cancel a release

> [!IMPORTANT]
> You can only cancel a release under the **Scheduled** status. You can't cancel a release under the **Active**, **Inactive, or **Paused** statuses.

**To cancel a release:**

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** from the left navigation menu.
1. Under the **Manage updates** section, select **Windows updates**.
1. In the **Windows updates** blade, select the **Feature updates** tab.
1. In the **Feature updates** tab, select the **horizontal ellipses (…)** > **Cancel** to cancel your feature updates release.
1. Select a reason for cancellation from the dropdown menu.
1. Optional. Enter details about why you're pausing or resuming the selected update.
1. Select **Cancel deployment** to save your changes.

## Pause and resume a release

> [!IMPORTANT]
> **Pausing or resuming an update can take up to eight hours to be applied to devices**. Windows Autopatch uses Microsoft Intune as its device management solution and that's the average frequency Windows devices take to communicate back to Microsoft Intune with new instructions to pause, resume, or rollback updates. For more information, see [how long does it take for devices to get a policy, profile, or app after they're assigned from Microsoft Intune](/intune/intune-service/configuration/device-profile-troubleshoot#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

**To pause and resume a release:**

> [!NOTE]
> If you pause an update, the specified release has the **Paused** status. You must select **Resume** to resume the update.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** from the left navigation menu.
1. Under the **Manage updates** section, select **Windows updates**.
1. In the **Windows updates** blade, select the **Feature updates** tab.
1. In the **Feature updates** tab, select the **horizontal ellipses (…)** > **Pause** or **Resume** to pause or resume your feature updates release.
1. Select a reason from the dropdown menu.
1. Optional. Enter details about why you're pausing or resuming the selected update.
1. If you're resuming an update, you can select one or more deployment rings.
1. Select **Pause deployment** or **Resume deployment** to save your changes.

## Roll back a release

Windows Autopatch doesn't support the rollback of Windows feature updates through its end-user experience flows.
