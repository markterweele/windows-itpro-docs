---
title: Post-device registration readiness checks
description: This article details how post-device registration readiness checks are performed in Windows Autopatch
ms.date: 03/31/2025
ms.service: windows-client
ms.subservice: autopatch
ms.topic: concept-article
ms.localizationpriority: medium
author: tiaraquan
ms.author: tiaraquan
manager: bpardi
ms.reviewer: andredm7
ms.collection:
  - highpri
  - tier1
---

# Post-device registration readiness checks

One of the most expensive aspects of the software update management process is to make sure devices are always healthy to receive and report software updates for each software update release cycle.

Having a way of measuring, quickly detecting and remediating when something goes wrong with ongoing change management processes is important; it helps mitigate high Helpdesk ticket volumes, reduces cost, and improves overall update management results.

Windows Autopatch provides proactive device readiness information about devices that are and aren't ready to be fully managed by the service. IT admins can easily detect and fix device-related issues that are preventing them from achieving their update management compliance report goals.

## Device readiness scenarios

Device readiness in Windows Autopatch is divided into two different scenarios:

| Scenario | Description |
| ----- | ----- |
| Prerequisite checks | Ensures devices follow software-based requirements before being registered with the service. |
| Post-device registration readiness checks | Provides continuous monitoring of device health for registered devices.<br><p>IT admins can easily detect and remediate configuration mismatches in their environments or issues that prevent devices from having one or more software update workloads fully managed by the Windows Autopatch service. Software workloads include:<ul><li>Windows quality updates</li><li>Feature updates</li><li>Microsoft Office</li><li>Microsoft Teams</li><li> Microsoft Edge</li></ul><p>Configuration mismatches can leave devices in a vulnerable state, out of compliance and exposed to security threats.</p></p>|

### Device readiness checks available for each scenario

| Required device readiness (prerequisite checks) before device registration (powered by Intune Graph API)  | Required post-device registration readiness checks (powered by Microsoft Cloud Managed Desktop Extension and Windows Autopatch Client Broker) |
| ----- | ----- |
| <ul><li>Windows OS (build, architecture, and edition)</li></li><li>Managed by either Intune or ConfigMgr co-management</li><li>ConfigMgr co-management workloads</li><li>Last communication with Intune</li><li>Personal or non-Windows devices</li></ul> | <ul><li>Windows OS (build, architecture, and edition)</li><li>Windows updates & Office Group Policy Object (GPO) versus Intune mobile device management (MDM) policy conflict</li><li>Bind network endpoints (Microsoft Defender, Microsoft Teams, Microsoft Edge, Microsoft Office)</li><li>Internet connectivity</li></ul> |

The status of each post-device registration readiness check is shown in the Windows Autopatch's Devices blade under the **Not registered** tab. You can take appropriate actions on devices that aren't ready to be fully managed by the Windows Autopatch service.

## Devices blade: Registered and Not registered tabs

You deploy software updates to secure your environment, but these deployments only reach healthy and active devices. Unhealthy or not ready devices affect the overall software update compliance.

Figuring out device health can be challenging and disruptive to the end user when IT admins can't:

- Obtain proactive data sent by the device to the service, or
- Proactively detect and remediate issues

Windows Autopatch has devices readiness states within its [**Autopatch group membership report**](../deploy/windows-autopatch-register-devices.md#autopatch-groups-membership-report). Each state provides IT admins monitoring information on which devices might have potential device health issues.

| Tab | Description |
| ----- | ----- |
| Registered |<ul><li>**Ready**</li><ul><li>Passed the prerequisite checks</li><li>Registered with Windows Autopatch</li><li>No active alerts targeted to the device</li></ul><li>**Not Ready**</li><ul><li>Devices that didn’t pass one or more post-device registration readiness checks</li><li>Devices that didn't communicate with the Microsoft Intune service in the last 28 days</li></ul></ul> |
| Not registered |<ul><li>**Prerequisite failed**<ul><li>Devices with the **Prerequisite failed** status didn't pass one or more prerequisite checks during the device registration process.</li></ul><li>**Excluded**</li><ul><li>Devices with the Excluded status are removed from the Windows Autopatch service</li></ul></ul>|

## Details about the post-device registration readiness checks

A healthy or active device in Windows Autopatch is:

- Online
- Actively sending data
- Passes all post-device registration readiness checks

The post-device registration readiness checks are powered by the **Microsoft Cloud Managed Desktop Extension**. It's installed right after devices are successfully registered with Windows Autopatch. The **Microsoft Cloud Managed Desktop Extension** and **Windows Autopatch Client Broker** has the Device Readiness Check Plugin. The Device Readiness Check Plugin is responsible for performing the readiness checks and reporting the results back to the service. The **Microsoft Cloud Managed Desktop Extension** and **Windows Autopatch Client Broker** are subcomponents of the overall Windows Autopatch service.

### Install the Windows Autopatch Client Broker

You can install the Windows Autopatch Client Broker on-demand at the tenant level to determine device update readiness and collect logs for issue triaging.

**To install the Windows Autopatch Client Broker**:

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Navigate to the **Tenant administration** menu.
1. In the **Windows Autopatch** section, select **Tenant Management**. Then, select **Manage client broker**.

The following list of post-device registration readiness checks is performed in Windows Autopatch:

| Check | Description |
| ----- | ----- |
| **Windows OS build, architecture, and edition** | Checks to see if devices support Windows 1809+ build (10.0.17763), 64-bit architecture and either Pro or Enterprise SKUs. |
| **Windows update policies managed via Microsoft Intune** | Checks to see if devices have Windows Updates policies managed via Microsoft Intune (MDM). |
| **Windows update policies managed via Group Policy Object (GPO)** | Checks to see if devices have Windows update policies managed via GPO. Windows Autopatch doesn't support Windows update policies managed via GPOs. Windows update must be managed via Microsoft Intune. |
| **Microsoft Office update policy managed via Group Policy Object (GPO)** | Checks to see if devices have Microsoft Office updates policies managed via GPO. Windows Autopatch doesn't support Microsoft Office update policies managed via GPOs. Office updates must be managed via Microsoft Intune or another Microsoft Office policy management method where Office update bits are downloaded directly from the Office Content Delivery Network (CDN). |
| **Windows Autopatch network endpoints** | There's a set of [network endpoints](../prepare/windows-autopatch-configure-network.md) that Windows Autopatch services must be able to reach for the various aspects of the Windows Autopatch service. |
| **Microsoft Teams network endpoints** | There's a set of [network endpoints](../prepare/windows-autopatch-configure-network.md) that devices with Microsoft Teams must be able to reach for software updates management. |
| **Microsoft Edge network endpoints** | There's a set of [network endpoints](../prepare/windows-autopatch-configure-network.md) that devices with Microsoft Edge must be able to reach for software updates management. |
| **Internet connectivity** | Checks to see if a device has internet connectivity to communicate with Microsoft cloud services. Windows Autopatch uses the PingReply class. Windows Autopatch tries to ping at least three different Microsoft's public URLs two times each, to confirm that ping results aren't coming from the device's cache. |

## Post-device registration readiness checks workflow

See the following diagram for the post-device registration readiness checks workflow:

:::image type="content" source="../media/windows-autopatch-post-device-registration-readiness-checks.png" alt-text="Post-device registration readiness checks" lightbox="../media/windows-autopatch-post-device-registration-readiness-checks.png":::

| Step | Description |
| ----- | ----- |
| **Steps 1-7** | For more information, see the [Device registration overview diagram](windows-autopatch-device-registration-overview.md).|
| **Step 8: Perform readiness checks** |<ol><li>Once devices are successfully registered with Windows Autopatch, the devices are added to the **Ready** tab.</li><li>The Microsoft Cloud Managed Desktop Extension and Windows Autopatch Client Broker agents perform readiness checks against devices in the **Ready** tab every 24 hours.</li></ol> |
| **Step 9: Check readiness status** |<ol><li>The Microsoft Cloud Managed Desktop Extension and Windows Autopatch Client Broker service evaluates the readiness results gathered by its agent.</li><li>The readiness results are sent from the Microsoft Cloud Managed Desktop Extension and Windows Autopatch Client Broker service component to the Device Readiness component within the Windows Autopatch's service.</li></ol>|
| **Step 10: Add devices to the Not ready** | When devices don't pass one or more readiness checks, even if they're registered with Windows Autopatch, they're added to the **Not ready** tab so IT admins can remediate devices based on Windows Autopatch recommendations. |
| **Step 11: IT admin understands what the issue is and remediates** | The IT admin checks and remediates issues in the Devices blade (**Not ready** tab). It can take up to 24 hours for devices to show in the **Ready** tab. |

## FAQ

| Question | Answer |
| ----- | ----- |
| **How frequent are the post-device registration readiness checks performed?** |<ul><li>The **Microsoft Cloud Managed Desktop Extension** and **Windows Autopatch Client Broker** agents collect device readiness statuses when it runs (once a day).</li><li>Once the agent collects results for the post-device registration readiness checks, it generates readiness results in the device in the `%programdata%\Microsoft\CMDExtension\Plugins\DeviceReadinessPlugin\Logs\DRCResults.json.log`.</li><li>The readiness results are sent over to **Microsoft Cloud Managed Desktop Extension** and **Windows Autopatch Client Broker** service.</li><li>The **Microsoft Cloud Managed Desktop Extension** and **Windows Autopatch Client Broker** service component sends the readiness results to the Device Readiness component. The results appear in the Windows Autopatch Devices blade (**Not ready** tab).</li></ul>|
| **What to expect when one or more checks fail?** | Devices are automatically sent to the **Ready** tab once they're successfully registered with Windows Autopatch. When devices don't meet one or more post-device registration readiness checks, the devices are moved to the **Not ready** tab. IT admins can learn about these devices and take appropriate actions to remediate them. Windows Autopatch provides information about the failure and how to potentially remediate devices.<p>Once devices are remediated, it can take up to **24 hours** to appear in the **Ready** tab.</p>|

## Additional resources

- [Device registration overview](../deploy/windows-autopatch-device-registration-overview.md)
- [Register your devices](../deploy/windows-autopatch-register-devices.md)
