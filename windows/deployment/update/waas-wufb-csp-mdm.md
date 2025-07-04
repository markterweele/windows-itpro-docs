---
title: Configure Windows Update client policies by using CSPs and MDM
description: Walk through demonstration of how to configure Windows Update client policies using Configuration Service Providers and MDM.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: bpardi
ms.localizationpriority: medium
appliesto:
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
ms.date: 03/18/2025
---

# Walkthrough: Use CSPs and MDMs to configure Windows Update client policies

> **Looking for consumer information?** See [Windows Update: FAQ](https://support.microsoft.com/windows/windows-update-faq-8a903416-6f45-0718-f5c7-375e92dddeb2).

## Overview

You can use Configuration Service Provider (CSP) policies to control how Windows Update client policies work by using a Mobile Device Management (MDM) tool. You should consider and devise a deployment strategy for updates before you make changes to the Windows Update client policies.

> [!TIP]
> This feature was formerly known as _Windows Update for Business_.

An IT administrator can configure Windows Update client policies by using Microsoft Intune or a non-Microsoft MDM tool.

To manage updates with Windows Update client policies, you should prepare with these steps, if you haven't already:

- Create Active Directory security groups that align with the deployment rings you use to phase deployment of updates. See [Build deployment rings for Windows client updates](waas-deployment-rings-windows-10-updates.md) to learn more about deployment rings in Windows client.
- Allow access to the Windows Update service.


## Manage Windows Update offerings

You can control when updates are applied, for example by deferring when an update is installed on a device or by pausing updates for a certain period of time.

### Determine which updates you want offered to your devices

Both feature and quality updates are automatically offered to devices that are connected to Windows Update using Windows Update client policies. However, you can choose whether you want the devices to additionally receive other Microsoft Updates or drivers that are applicable to that device.

To enable Microsoft Updates, use [Update/AllowMUUpdateService](/windows/client-management/mdm/policy-csp-update#allowmuupdateservice).

Drivers are automatically enabled because they're beneficial to device systems. We recommend that you allow the driver policy to allow drivers to be updated on devices (the default), but you can turn off this setting if you prefer to manage drivers manually. If you want to disable driver updates for some reason, use Update/[ExcludeWUDriversInQualityUpdate](/windows/client-management/mdm/policy-csp-update#excludewudriversinqualityupdate).

 We also recommend that you allow Microsoft product updates as discussed previously.

### Set when devices receive feature and quality updates

#### I want to receive prerelease versions of the next feature update

1. Ensure that you're enrolled in the Windows Insider Program for Business. Windows Insider is a free program available to commercial customers to aid them in their validation of feature updates before they're released. Joining the program enables you to receive updates prior to their release as well as receive emails and content related to what is coming in the next updates.

1. For any of test devices you want to install prerelease builds, use [Update/ManagePreviewBuilds](/windows/client-management/mdm/policy-csp-update#managepreviewbuilds). Set the option to **Enable preview builds**.

1. Use [Update/BranchReadinessLevel](/windows/client-management/mdm/policy-csp-update#branchreadinesslevel) and select one of the preview Builds. Windows Insider Program Slow is the recommended channel for commercial customers who are using prerelease builds for validation.

1. Additionally, you can defer prerelease feature updates the same way as released updates, by setting a deferral period up to 14 days by using [Update/DeferFeatureUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferfeatureupdatesperiodindays). If you're testing with Windows Insider Program Slow builds, we recommend that you receive the preview updates to your IT department on day 0, when the update is released, and then have a 7-10 day deferral before rolling out to your group of testers. This schedule helps ensure that if a problem is discovered, you can pause the rollout of the preview update before it reaches your tests.

#### I want to manage which released feature update my devices receive

A Windows Update administrator can defer or pause updates. You can defer feature updates for up to 365 days and defer quality updates for up to 30 days. Deferring simply means that you don't receive the update until it has been released for at least the number of deferral days you specified (offer date = release date + deferral date). You can pause feature or quality updates for up to 35 days from a given start date that you specify.

- To defer a feature update: [Update/DeferFeatureUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferfeatureupdatesperiodindays)
- To pause a feature update: [Update/PauseFeatureUpdatesStartTime](/windows/client-management/mdm/policy-csp-update#pausefeatureupdatesstarttime)
- To defer a quality update: [Update/DeferQualityUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferqualityupdatesperiodindays)
- To pause a quality update: [Update/PauseQualityUpdatesStartTime](/windows/client-management/mdm/policy-csp-update#pausequalityupdatesstarttime)

#### Example

In this example, there are three rings for quality updates. The first ring ("pilot") has a deferral period of 0 days. The second ring ("fast") has a deferral of five days. The third ring ("slow") has a deferral of ten days.

![illustration of devices divided into three rings.](images/waas-wufb-3-rings.png)

When the quality update is released, it's offered to devices in the pilot ring the next time they scan for updates.

##### Five days later
The devices in the fast ring are offered the quality update the next time they scan for updates.

![illustration of devices with fast ring deployed.](images/waas-wufb-fast-ring.png)

##### Ten days later
Ten days after the quality update is released, it's offered to the devices in the slow ring the next time they scan for updates.

![illustration of devices with slow ring deployed.](images/waas-wufb-slow-ring.png)

If no problems occur, all of the devices that scan for updates are offered the quality update within ten days of its release, in three waves.

##### What if a problem occurs with the update?

In this example, some problem is discovered during the deployment of the update to the "pilot" ring.

![illustration of devices divided with pilot ring experiencing a problem.](images/waas-wufb-pilot-problem.png)

At this point, the IT administrator can set a policy to pause the update. In this example, the admin selects the **Pause quality updates** check box.

![illustration of rings with pause quality update check box selected.](images/waas-wufb-pause.png)

Now all devices are paused from updating for 35 days. When the pause is removed, they'll be offered the *next* quality update, which ideally won't have the same issue. If there's still an issue, the IT admin can pause updates again.




#### I want to stay on a specific version

If you need a device to stay on a version beyond the point when deferrals on the next version would elapse or if you need to skip a version (for example, update fall release to fall release) use the [Update/TargetReleaseVersion](/windows/client-management/mdm/policy-csp-update#targetreleaseversion) (or Deploy Feature Updates Preview in Intune) instead of using feature update deferrals. When you use this policy, specify the version that you want your device(s) to move to or stay on (for example, "1909"). You can find version information at the [Windows 10 Release Information Page](/windows/release-health/release-information).

## Manage how users experience updates

### I want to manage when devices download, install, and restart after updates

We recommended that you allow updating automatically, which is the default behavior. If you don't set an automatic update policy, the device attempts to download, install, and restart at the best times for the user by using built-in intelligence such as intelligent active hours.

For more granular control, you can set the maximum period of active hours the user can set with [Update/ActiveHoursMaxRange](/windows/client-management/mdm/policy-csp-update#activehoursmaxrange). You could also set specific start and end times for active ours with [Update/ActiveHoursEnd](/windows/client-management/mdm/policy-csp-update#activehoursend) and [Update/ActiveHoursStart](/windows/client-management/mdm/policy-csp-update#activehoursstart).

It's best to refrain from setting the active hours policy because it's enabled by default when automatic updates aren't disabled and provides a better experience when users can set their own active hours.

To update outside of the active hours, use [Update/AllowAutoUpdate](/windows/client-management/mdm/policy-csp-update#allowautoupdate) with Option 2 (which is the default setting). For even more granular control, consider using automatic updates to schedule the install time, day, or week. To use a schedule, use Option 3, and then set the following policies as appropriate for your plan:

- [Update/ScheduledInstallDay](/windows/client-management/mdm/policy-csp-update#scheduledinstallday)
- [Update/ScheduledInstallEveryWeek](/windows/client-management/mdm/policy-csp-update#scheduledinstalleveryweek)
- [Update/ScheduledInstallFirstWeek](/windows/client-management/mdm/policy-csp-update#scheduledinstallfirstweek)
- [Update/ScheduledInstallFourthWeek](/windows/client-management/mdm/policy-csp-update#scheduledinstallfourthweek)
- [Update/ScheduledInstallSecondWeek](/windows/client-management/mdm/policy-csp-update#scheduledinstallsecondweek)
- [Update/ScheduledInstallThirdWeek](/windows/client-management/mdm/policy-csp-update#scheduledinstallthirdweek)
- [Update/ScheduledInstallTime](/windows/client-management/mdm/policy-csp-update#scheduledinstalltime)


When you set these policies, installation happens automatically at the specified time and the device will restart 15 minutes after installation is complete (unless it's interrupted by the user).

If you don't want to allow any automatic updates prior to the deadline, set [Update/AllowAutoUpdate](/windows/client-management/mdm/policy-csp-update#allowautoupdate) to Option 5, which turns off automatic updates.

### I want to keep devices secure and compliant with update deadlines

We recommend that you use set specific deadlines for feature and quality updates to ensure that devices stay secure on Windows 10, version 1709 and later. Deadlines work by enabling you to specify the number of days that can elapse after an update is offered to a device before it must be installed. Also you can set the number of days that can elapse after a pending restart before the user is forced to restart. For more information about these settings, see [Enforcing compliance deadlines for updates](wufb-compliancedeadlines.md). The following settings enforce compliance deadlines for updates:

For Windows 10, version 22H2:

- [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforfeatureupdates)
- [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforqualityupdates)
- [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update#update-configuredeadlinegraceperiod)
- [Update/ConfigureDeadlineGracePeriodForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiodforfeatureupdates)
- [Update/ConfigureDeadlineNoAutoReboot](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautoreboot)

For Windows 11, version 22H2 and later:

- [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforfeatureupdates)
- [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforqualityupdates)
- [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update#update-configuredeadlinegraceperiod) (for quality updates)
- [Update/ConfigureDeadlineGracePeriodForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiodforfeatureupdates) <!--Windows 11, version 22H2 and later-->
- [Update/ConfigureDeadlineNoAutoRebootForQualityUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautorebootforqualityupdates) <!--Windows 11, version 22H2 and later-->
- [Update/ConfigureDeadlineNoAutoRebootForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautorebootforfeatureupdates) <!--Windows 11, version 22H2 and later-->

> [!NOTE]
> - When these policies are used, [user settings for notifications](#user-settings-for-notifications) are also used on clients running Windows 11, version 22H2 and later.
> - When **Specify deadlines for automatic updates and restarts** for either quality updates or feature updates is used, updates will be downloaded and installed as soon as they are offered.
> - When **Specify deadlines for automatic updates and restarts** for either quality updates or feature updates is used, download, installation, and reboot settings stemming from the [Configure Automatic Updates](waas-restart.md#schedule-update-installation) are ignored.
>    - Starting with the December 10, 2024 update for Windows 11, version 22H2 and later clients, [Configure Automatic Updates](waas-restart.md#schedule-update-installation) are respected before the deadline occurs, and ignored once the deadline passes.


### <a name="user-settings-for-notifications"></a> End user settings for notifications
<!--8936877-->
*Applies to:*
- Windows 11, version 23H2 with [KB5037771](https://support.microsoft.com/help/5037771) or later
- Windows 11, version 22H2 with [KB5037771](https://support.microsoft.com/help/5037771) or later

Users can set a preference for notifications about pending restarts for updates under **Settings** > **Windows Update** > **Advanced options** > **Notify me when a restart is required to finish updating**. This setting is end-user controlled and not controlled or configurable by IT administrators.

Users have the following options for the **Notify me when a restart is required to finish updating** setting:

- **Off** (default): Once the device enters a pending reboot state for updates, restart notifications are suppressed for 24 hours. During the first 24 hours, automatic restarts can still occur outside of active hours. Typically, users receive fewer notifications about upcoming restarts while the deadline is approaching.
    - When the deadline is set for 1 day, users only receive a notification about the deadline and a final nondismissable notification 15 minutes before a forced restart.

- **On**: Users immediately receive a toast notification when the device enters a reboot pending state for updates. Automatic restarts for updates are blocked for 24 hours after the initial notification to give these users time to prepare for a restart. After 24 hours have passed, automatic restarts can occur. This setting is recommended for users who want to be notified about upcoming restarts.
   - When the deadline is set for 1 day, an initial notification occurs, automatic restart is blocked for 24 hours, and users receive another notification before the deadline and a final nondismissable notification 15 minutes before a forced restart.

When a deadline is set for 0 days, no matter which option is selected, the only notification users receive is a final nondismissable notification 15 minutes before a forced restart.

The user preference for notifications applies when the following policies for [compliance deadlines](wufb-compliancedeadlines.md) are used:

For Windows 10, version 22H2:

- [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforfeatureupdates)
- [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforqualityupdates)
- [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update#update-configuredeadlinegraceperiod)
- [Update/ConfigureDeadlineGracePeriodForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiodforfeatureupdates)
- [Update/ConfigureDeadlineNoAutoReboot](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautoreboot)

For Windows 11, version 22H2 and later:

- [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforfeatureupdates)
- [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforqualityupdates)
- [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update#update-configuredeadlinegraceperiod) (for quality updates)
- [Update/ConfigureDeadlineGracePeriodForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiodforfeatureupdates) <!--Windows 11, version 22H2 and later-->
- [Update/ConfigureDeadlineNoAutoRebootForQualityUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautorebootforqualityupdates) <!--Windows 11, version 22H2 and later-->
- [Update/ConfigureDeadlineNoAutoRebootForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautorebootforfeatureupdates) <!--Windows 11, version 22H2 and later-->


### I want to manage the notifications a user sees

There are additional settings that affect the notifications.

We recommend that you use the default notifications as they aim to provide the best user experience while adjusting for the compliance policies that you set. If you do have further needs that aren't met by the default notification settings, you can use the [Update/NoUpdateNotificationsDuringActiveHours](/windows/client-management/mdm/policy-csp-update#NoUpdateNotificationsDuringActiveHours) policy with these values:

**0** (default) - Use the default Windows Update notifications<br/>
**1** - Turn off all notifications, excluding restart warnings<br/>
**2** - Turn off all notifications, including restart warnings

> [!NOTE]
> Option **2** creates a poor experience for personal devices; it's only recommended for kiosk devices where automatic restarts have been disabled.

Still more options are available in [Update/ScheduleRestartWarning](/windows/client-management/mdm/policy-csp-update#schedulerestartwarning). This setting allows you to specify the period for auto restart warning reminder notifications (from 2-24 hours; 4 hours is the default) before the update. You can also specify the period for auto restart imminent warning notifications with [Update/ScheduleImminentRestartWarning](/windows/client-management/mdm/policy-csp-update#scheduleimminentrestartwarning) (15-60 minutes is the default). We recommend using the default notifications.

### I want to manage the update settings a user can access

Every Windows device provides users with various controls they can use to manage Windows Updates. They can access these controls by Search to find Windows Updates or by going selecting **Updates and Security** in **Settings**. We provide the ability to disable a variety of these controls that are accessible to users.

Users with access to update pause settings can prevent both feature and quality updates for 7 days. You can prevent users from pausing updates through the Windows Update settings page by using [Update/SetDisablePauseUXAccess](/windows/client-management/mdm/policy-csp-update#setdisablepauseuxaccess).
When you disable this setting, users see **Some settings are managed by your organization** and the update pause settings are greyed out.

If you use Windows Server Update Server (WSUS), you can prevent users from scanning Windows Update. To do this, use [Update/SetDisableUXWUAccess](/windows/client-management/mdm/policy-csp-update#setdisableuxwuaccess).



### I want to enable features introduced via servicing that are off by default
<!--6544872-->
(*Starting in Windows 11, version 22H2 or later*)

New features and enhancements are introduced through the monthly cumulative update to provide continuous innovation for Windows 11. To give organizations time to plan and prepare, some of these new features are temporarily turned off by default. Features that are turned off by default are listed in the KB article for the monthly cumulative update. Typically, a feature is selected to be off by default because it either impacts the user experience or IT administrators significantly.

The features that are turned off by default from servicing updates will be enabled in the next annual feature update. Organizations can choose to deploy feature updates at their own pace, to delay these features until they're ready for them.

 You can enable these features by using [AllowTemporaryEnterpriseFeatureControl](/windows/client-management/mdm/policy-csp-update?toc=/windows/deployment/toc.json&bc=/windows/deployment/breadcrumb/toc.json#allowtemporaryenterprisefeaturecontrol). The following options are available:

- **0** (default): Not allowed. Features that are shipped turned off by default will remain off
- **1**: Allowed. All features in the latest monthly cumulative update are enabled.
  - When the policy is set to **1**, all features that are currently turned off will turn on when the device next reboots.

### I want to enable optional updates
<!--7991583-->
*Applies to:*
- Windows 11, version 22H2 with [KB5029351](https://support.microsoft.com/help/5029351) and later <!--7991583-->
- Windows 10, version 22H2 with [KB5032278](https://support.microsoft.com/help/5032278), or a later cumulative update installed <!--8503602-->

In addition to the monthly cumulative update, optional updates are available to provide new features and nonsecurity changes. Most optional updates are released on the fourth Tuesday of the month, known as optional nonsecurity preview releases. Optional updates can also include features that are gradually rolled out, known as controlled feature rollouts (CFRs). Installation of optional updates isn't enabled by default for devices that receive updates using Windows Update client policies. However, you can enable optional updates for devices by using [AllowOptionalContent](/windows/client-management/mdm/policy-csp-update?toc=/windows/deployment/toc.json&bc=/windows/deployment/breadcrumb/toc.json#allowoptionalcontent). For more information about optional content, see [Enable optional updates](waas-configure-wufb.md#enable-optional-updates).