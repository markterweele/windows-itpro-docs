---
title: Enable Extended Security Updates (ESU)
description: Learn how to enable the Extended Security Updates (ESU) keys for Windows 10. The ESU program gives customers the option to receive security updates for Windows 10.
ms.service: windows-client
ms.subservice: itpro-fundamentals
ms.author: mstewart
author: mestew
manager: bpardi
ms.localizationpriority: medium
ms.topic: article
ms.date: 05/21/2025
ms.collection:
  - highpri
  - tier2
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10, version 22H2</a>
---

# Enable Extended Security Updates (ESU)
<!--10014911-->
> **Looking for consumer information?** For individuals or Windows 10 Home customers, more information about Extended Security Updates for Windows 10 is available in the frequently asked questions section of the [End of support for Windows 10](https://www.microsoft.com/windows/end-of-support) page.<!--10013381-->

The [Windows 10 Extended Security Updates (ESU) program](extended-security-updates.md) allows organizations to receive critical and important security updates for PCs enrolled in the paid subscription service. ESU extends the use of Windows 10 devices past the end of support date on October 14, 2025. This article provides instructions on how to enable the ESU keys in commercial environments.

## Prerequisites

To enable ESU for Windows 10, you must meet the following prerequisites:

**Client operating system:**
- Windows 10, version 22H2 with [KB5046613](https://support.microsoft.com/help/5046613), or a later update installed
- Administrative privileges on the device

**Endpoints for client activation:**
- `https://go.microsoft.com/`
- `https://login.live.com`
- `https://activation.sls.microsoft.com/`
- `http://crl.microsoft.com/`
- `https://validation.sls.microsoft.com/`
- `https://activation-v2.sls.microsoft.com/`
- `https://validation-v2.sls.microsoft.com/`
- `https://displaycatalog.mp.microsoft.com/`
- `https://licensing.mp.microsoft.com/`
- `https://purchase.mp.microsoft.com/`
- `https://displaycatalog.md.mp.microsoft.com/`
- `https://licensing.md.mp.microsoft.com/`
- `https://purchase.md.mp.microsoft.com/`

**Microsoft 365 admin center:**

- [Volume licensing access](/microsoft-365/commerce/licenses/vl-sign-in) in the [Microsoft 365 admin center](https://admin.microsoft.com)

## Get the product keys for activating Extended Security Update (ESU) licenses

If you bought ESU licenses, you can activate them with Multiple Activation Keys (MAK) that you get from the Microsoft 365 admin center. To find the ESU license MAK, use the following steps:

1. In the [admin center](https://admin.microsoft.com), go to the **Billing** > **Your Products** page, then select the <a href="https://go.microsoft.com/fwlink/p/?linkid=2244144" target="_blank">Volume licensing</a> tab.
2. In the **Contracts** section, select **View contracts**.
3. On the <a href="https://go.microsoft.com/fwlink/p/?linkid=2297440" target="_blank">Contracts</a> page, find the **License ID** that the ESU licenses were purchased under, select the three dots (**More actions**), then select **View product keys**. The **Product keys** details page includes contract details and a list of all keys for that contract.

> [!NOTE]
> You can order ESU licenses before the start of the ESU coverage period. However, the ESU MAK displayed in the Product keys details panel isn't usable until the defined ESU coverage period begins. For more information, see [Product Lifecycle FAQ - Extended Security Updates](/lifecycle/faq/extended-security-updates).

## Install and activate the ESU key

You manage licensing and activation on devices using [slmgr.vbs](/windows-server/get-started/activation-slmgr-vbs-options). The device needs access to the internet and to Microsoft Activation Servers. If the device can't access either the internet or the Microsoft Activation Servers, see [Activate ESU keys by phone](#activate-esu-keys-by-phone). To install the ESU key on clients, use the following steps:

1. Open an elevated Command Prompt window on the device.
1. Run the following command to install the ESU key, replacing `<ESU MAK>` with the actual ESU MAK you obtained from the Microsoft 365 admin center:

   ```cmd
   slmgr.vbs /ipk <ESU MAK>
   ```

   After you run this command, you should see a Windows Script Host dialog box that states the product key was installed successfully.
1. Find the ESU Activation ID using the following table:

   | ESU Program | Activation ID |
   |---|---|
   |Win10 ESU Year1| f520e45e-7413-4a34-a497-d2765967d094 |
   |Win10 ESU Year2| 1043add5-23b1-4afb-9a0f-64343c8f3f8d |
   |Win10 ESU Year3| 83d49986-add3-41d7-ba33-87c7bfb5c0fb |

   > [!Note]
   > The activation IDs are the same across all eligible Windows ESU editions and all devices enrolled for that program.
1. From the elevated Command Prompt window, run the following command to activate the ESU key, replacing `<Activation ID>` with the actual ESU Activation ID you obtained in the previous step:

   ```cmd
   slmgr.vbs /ato <Activation ID>
   ```

   After you run this command, you should see a Windows Script Host dialog box that states the product was activated successfully.
1. To verify that the ESU key is installed and activated, run the following command from an elevated Command Prompt:

   ```cmd
   slmgr.vbs /dlv
   ```

   The output should show the **Name** of the corresponding ESU program and the **License Status** as `Licensed` for that program.

## Activate ESU keys by phone

If the device doesn't have access to the internet or to the Microsoft Activation Servers, use the following steps fo a manual phone activation:

1. Open an elevated Command Prompt window on the device. You'll be managing licensing and activation on devices using [slmgr.vbs](/windows-server/get-started/activation-slmgr-vbs-options).
1. Run the following command to install the ESU key, replacing `<ESU MAK>` with the actual ESU MAK you obtained in the previous section:

   ```cmd
   slmgr.vbs /ipk <ESU MAK>
   ```

   After you run this command, you should see a Windows Script Host dialog box that states the product key was installed successfully.
1. To verify that the ESU key is installed, run the following command from an elevated Command Prompt:

   ```cmd
   slmgr.vbs /dlv
   ```

   > [!Note]
   > The activation IDs are the same across all eligible Windows ESU editions and all devices enrolled for that program.
1. Find the ESU Activation ID using the following table:

   | ESU Program | Activation ID |
   |---|---|
   |Win10 ESU Year1| f520e45e-7413-4a34-a497-d2765967d094 |
   |Win10 ESU Year2| 1043add5-23b1-4afb-9a0f-64343c8f3f8d |
   |Win10 ESU Year3| 83d49986-add3-41d7-ba33-87c7bfb5c0fb |

   > [!Note]
   > The activation IDs are the same across all eligible Windows ESU editions and all devices enrolled for that program.
1. Get the **Installation ID (IID)** from the device by run the following command in  an elevated Command Prompt, replacing `<Activation ID>` with the actual ESU Activation ID you obtained in the previous step:

   ```cmd
   slmgr.vbs /dti <Activation ID>
   ```
1. Once you have the **Installation ID**, call the [Microsoft Licensing Activation Center](https://www.microsoft.com/Licensing/existing-customer/activation-centers) for your region. They'll walk you through the steps to get the **Confirmation ID**. Make a note of your **Confirmation ID**. You can also request to receive a text message with a link to a web page where you can look up your **Confirmation ID** by entering the **Installation ID**. The link can only be used for two devices at a time.
1. From the elevated Command Prompt window, run the following command to activate the ESU key, replacing `<Activation ID>` with the actual ESU Activation ID you obtained from the chart and `<Confirmation ID>` with the actual Confirmation ID you received from the Microsoft Licensing Activation Center:

   ```cmd
   slmgr.vbs /atp <Confirmation ID> <Activation ID>
   ```

   > [!Note]
   > The `<Confirmation ID>` shouldn't have spaces in it.
1. To verify that the ESU key is installed and activated, run the following command from an elevated Command Prompt:

   ```cmd
   slmgr.vbs /dlv
   ```

   The output should show the **Name** of the corresponding ESU program and the **License Status** as `Licensed` for that program.

## Activate large numbers of devices that don't have internet access

For more information on how to do manual activation of large numbers of devices, review the Volume Activation Management Tool (VAMT) [Proxy Activation](/windows/deployment/volume-activation/proxy-activation-vamt) scenario. You should install the latest [Automated Deployment Kit (ADK) tool](/windows-hardware/get-started/adk-install) to ensure that you have latest VAMT tool

Note:  In order to add Windows 10 ESU keys to VAMT update the pkeyconfig files with this update

[https://www.microsoft.com/en-us/download/details.aspx?id=106364](https://www.microsoft.com/download/details.aspx?id=106364)

For more information on adding additional activations to a Windows 10 ESU MAK, see [Request an increase to MAK activation limits](/microsoft-365/commerce/licenses/product-keys-for-vl#request-an-increase-to-mak-activation-limits).

## Related content

- [Slmgr.vbs options](/windows-server/get-started/activation-slmgr-vbs-options)
- [Extended Security Updates (ESU) program for Windows 10](extended-security-updates.md)