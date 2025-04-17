---
title: Manage Recall for Windows clients
description: Learn how to manage Recall for commercial environments and about Recall features.
ms.topic: how-to
ms.subservice: windows-copilot
ms.date: 04/22/2025
ms.author: mstewart
author: mestew
ms.collection:
  - windows-copilot
  - magic-ai-copilot
appliesto:
- ✅ <a href="https://www.microsoft.com/windows/business/devices/copilot-plus-pcs#copilot-plus-pcs" target="_blank">Copilot+ PCs</a>
---


# Manage Recall
<!--8908044, 9608247-->
>**Looking for consumer information?** See [Retrace your steps with Recall](https://support.microsoft.com/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c).

Recall (preview) allows users to search locally saved and locally analyzed snapshots of their screen using natural language. By default, Recall is disabled and removed on managed devices. IT admins can choose if they want to allow Recall to be used in their organizations and users, on their own, won't be able to enable it on their managed device if the Allow Recall policy is disabled. IT admins, on their own, can't start saving snapshots for end users. Recall is an opt-in experience that requires end user consent to save snapshots. Users can choose to enable or disable saving snapshots for themselves anytime. IT admins can only set policies that give users the option to enable saving snapshots and configure certain policies for Recall.

This article provides information about Recall and how to manage it in a commercial environment.

> [!NOTE]
> - In-market commercial devices are defined as devices with an Enterprise (ENT) or Education (EDU) SKU or any premium SKU device that is managed by an IT administrator (whether via Microsoft Endpoint Manager or other endpoint management solution), has a volume license key, or is joined to a domain. Commercial devices during Out of Box Experience (OOBE) are defined as those with ENT or EDU SKU or any premium SKU device that has a volume license key or is Microsoft Entra joined. 
> - Recall is optimized for select languages English, Chinese (simplified), French, German, Japanese, and Spanish. Content-based and storage limitations apply. For more information, see [https://aka.ms/copilotpluspcs](https://aka.ms/copilotpluspcs).

## What is Recall?

Recall (preview) allows you to search across time to find the content you need. Just describe how you remember it, and Recall retrieves the moment you saw it. Snapshots are taken periodically while content on the screen is different from the previous snapshot. The snapshots of your screen are organized into a timeline. Snapshots are locally stored and locally analyzed on your PC. Recall's analysis allows you to search for content, including both images and text, using natural language.

When Recall opens a snapshot you selected, it enables Click to Do, which runs on top of the saved snapshot. Click to Do analyzes what's in the snapshot and allows you to interact with individual elements in the snapshot. For instance, you can copy text from the snapshot or send pictures from the snapshot to an app that supports `jpeg` files.

:::image type="content" border="true" source="images/8908044-recall-search.png" alt-text="Screenshot of Recall with search results displayed for a query for a presentation with a red barn." lightbox="images/8908044-recall-search.png":::

### Recall security and privacy architecture

Privacy and security are built into Recall's design. With Copilot+ PCs, you get powerful AI that runs locally on the device. No internet or cloud connections are required or used to save and analyze snapshots. Snapshots aren't sent to Microsoft. Recall AI processing occurs locally, and snapshots are securely stored on the local device only. <!--9608247-->Any future options for the user to share data will require fully informed explicit action by the user.

Recall doesn't share snapshots with other users that are signed into Windows on the same device and IT admins can't access or view the snapshots on end-user devices. Microsoft can't access or view the snapshots. Recall requires users to confirm their identity with [Windows Hello](https://support.microsoft.com/windows/configure-windows-hello-dae28983-8242-bb2a-d3d1-87c9d265a5f0) before it launches and before accessing snapshots. At least one biometric sign-in option must be enabled for Windows Hello, either facial recognition or a fingerprint, to launch and use Recall. Before snapshots start getting saved to the device, users need to open Recall and authenticate. Recall takes advantage of just in time decryption protected by [Hello Enhanced Sign-in Security (ESS)](/windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security). Snapshots and any associated information in the vector database are always encrypted. Encryption keys are protected via Trusted Platform Module (TPM), which is tied to the user's Windows Hello ESS identity, and can be used by operations within a secure environment called a [Virtualization-based Security Enclave (VBS Enclave)](/windows/win32/trusted-execution/vbs-enclaves). This means that other users can't access these keys and thus can't decrypt this information. Device Encryption or BitLocker are enabled by default on Windows 11. For more information, see [Recall security and privacy architecture in the Windows Experience Blog](https://blogs.windows.com/windowsexperience/?p=179096).

When using Recall, the **Sensitive information filtering** setting is enabled by default to help ensure your data's confidentiality. This feature operates directly on your device, utilizing the NPU and the Microsoft Classification Engine (MCE) - the same technology leveraged by [Microsoft Purview](/purview/purview) for detecting and labeling sensitive information. When this setting is enabled, snapshots won't be saved when potentially sensitive information is detected. Most importantly, the sensitive information remains on the device at all times, regardless of whether the **Sensitive information filtering** setting is enabled or disabled. For more information about the types of potentially sensitive information, see [Reference for sensitive information filtering in Recall](recall-sensitive-information-filtering.md).

Like any Windows feature, some diagnostic data may be provided based on the user's privacy settings. For more information about diagnostic data, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization). Occasionally, Recall will get artifacts from the internet from the snapshot URL top-level domain. For example, it will get favicons (website icons) or other website metadata. Recall uses these items to give users a better experience when browsing the Recall timeline or search results.

### Click to Do privacy considerations  

Recall uses Click to Do, which allows the user to interact with the content in snapshots.

> [!IMPORTANT]
> The policy to manage Click to Do doesn't affect Click to Do in Recall. For more information, see [Manage Click to Do](manage-click-to-do.md). 

Click to Do can run on top of:

- The current screen when the **Now** button is selected
- Snapshots that have already been saved

For snapshots that have already been saved, info from filtered apps and websites along with private browsing activity from supported browsers is removed. Click to Do can't access info that was removed by filters when it's analyzing saved snapshots. When the **Now** option is selected, a snapshot is taken without private browsing windows, filtered apps, and filtered websites. These snapshots are displayed and locally analyzed but only saved if you have [saving snapshots enabled](#allow-recall-and-snapshots-policies). When using the **Now** option, Click to Do analyzes only what's active on the screen. It doesn't analyze content that's inside minimized apps that aren't on screen. 

[!Include [Click to Do privacy considerations](./includes/click-to-do-privacy.md)]


## System requirements

Recall has the following minimum requirements:

- A [Copilot+ PC](https://www.microsoft.com/windows/business/devices/copilot-plus-pcs#copilot-plus-pcs) that meets the [Secured-core standard](/windows-hardware/design/device-experiences/oem-highly-secure-11)
- 40 TOPs NPU ([neural processing unit](https://support.microsoft.com/windows/all-about-neural-processing-units-npus-e77a5637-7705-4915-96c8-0c6a975f9db4))
- 16 GB RAM
- 8 logical processors
- 256 GB storage capacity
  - To enable Recall, you need at least 50 GB of space free
  - Saving snapshots automatically pauses once the device has less than 25 GB of storage space
- Users need to enable Device Encryption or BitLocker
- Users need to enroll into [Windows Hello Enhanced Sign-in Security](/windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security) with at least one biometric sign-in option enabled in order to authenticate.

## Supported browsers

Users need a supported browser for Recall to [filter websites](#app-and-website-filtering-policies) and to automatically filter private browsing activity. Supported browsers, and their capabilities include:

- **Microsoft Edge**: filters specified websites and filters private browsing activity
- **Firefox**: filters specified websites and filters private browsing activity
- **Opera**: filtered specified websites and filters private browsing activity
- **Google Chrome**: filters specified websites and filters private browsing activity
- **Chromium based browsers** (124 or later): For Chromium-based browsers not listed, filters private browsing activity only, doesn't filter specific websites


## Configure policies for Recall

By default, Recall is removed on commercially managed devices. If you want to allow Recall to be available for users in your organization and allow them to choose to save snapshots, you need to configure both the **Allow Recall to be enabled** and **Turn off saving snapshots for Windows** policies. Policies for Recall fall into the following general areas:

- [Allow Recall and snapshots policies](#allow-recall-and-snapshots-policies)
- [Storage policies](#storage-policies)
    - Storage policies apply only to Enterprise and Education editions of Windows
- [App and website filtering policies](#app-and-website-filtering-policies)
    - Storage policies apply only to Enterprise and Education editions of Windows


### Allow Recall and snapshots policies

The **Allow Recall to be enabled** policy setting allows you to determine whether the Recall optional component is available for end users to enable on their device. By default, Recall is disabled and removed for managed devices. Recall isn't available on managed devices by default, and individual users can't enable Recall on their own. If you disable this policy, the Recall component will be in disabled state and the bits for Recall will be removed from the device. If snapshots were previously saved on the device, they'll be deleted when this policy is disabled. Removing Recall requires a device restart. If the policy is enabled, end users will have Recall available on their device. Depending on the state of the DisableAIDataAnalysis policy (Turn off saving snapshots for use with Recall), end users will be able to choose if they want to save snapshots of their screen and use Recall to find things they've seen on their device. Some Recall policies apply only to Enterprise and Education editions of Windows.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[AllowRecallEnablement](mdm/policy-csp-windowsai.md#allowrecallenablement) |
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Allow Recall to be enabled** |


The **Turn off saving snapshots for Windows** policy allows you to give the users the choice to save snapshots of their screen for use with Recall. Administrators can't enable saving snapshots on behalf of their users. The choice to enable saving snapshots requires individual user opt-in consent. By default, snapshots won't be saved for use with Recall. If snapshots were previously saved on a device, they'll be deleted when this policy is enabled. If you set this policy to disabled, end users will have a choice to save snapshots of their screen and use Recall to find things they've seen on their device.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[DisableAIDataAnalysis](mdm/policy-csp-windowsai.md#disableaidataanalysis) </br> </br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[DisableAIDataAnalysis](mdm/policy-csp-windowsai.md#disableaidataanalysis)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Turn off saving snapshots for Windows** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Turn off saving snapshots for Windows** |

### Storage policies

You can define how much disk space Recall can use by using the **Set maximum storage for snapshots used by Recall** policy. You can set the maximum amount of disk space for snapshots to be 10, 25, 50, 75, 100, or 150 GB. When the storage limit is reached, the oldest snapshots are deleted first. When this setting isn't configured, the OS configures the storage allocation for snapshots based on the device storage capacity. 25 GB is allocated when the device storage capacity is 256 GB. 75 GB is allocated when the device storage capacity is 512 GB. 150 GB is allocated when the device storage capacity is 1 TB or higher.

> [!NOTE]
> This setting applies only to Enterprise and Education editions of Windows.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageSpaceForRecallSnapshots](mdm/policy-csp-windowsai.md#setmaximumstoragespaceforrecallsnapshots) </br> </br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageSpaceForRecallSnapshots](mdm/policy-csp-windowsai.md#setmaximumstoragespaceforrecallsnapshots)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum storage for snapshots used by Recall** </br></br> User Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum storage for snapshots used by Recall** |

You can define how long snapshots can be retained on the device by using the **Set maximum duration for storing snapshots used by Recall** policy. You can configure the maximum storage duration to be 30, 60, 90, or 180 days. If the policy isn't configured, snapshots aren't deleted until the maximum storage allocation is reached, and then the oldest snapshots are deleted first.

> [!NOTE]
> This setting applies only to Enterprise and Education editions of Windows.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageDurationForRecallSnapshots](mdm/policy-csp-windowsai.md#setmaximumstoragedurationforrecallsnapshots) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageDurationForRecallSnapshots](mdm/policy-csp-windowsai.md#setmaximumstoragedurationforrecallsnapshots)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum storage for snapshots used by Recall** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum duration for storing snapshots used by Recall** |


### App and website filtering policies

You can filter both apps and websites from being saved in snapshots. Users are able to add to these filter lists from the **Recall & Snapshots** settings page. Some remote desktop connection clients are filtered by default from snapshots. For more information, see the [Remote desktop connection clients filtered from snapshots](#remote-desktop-connection-clients-filtered-from-snapshots) section.

To filter websites from being saved in snapshots, use the **Set a list of URIs to be filtered from snapshots for Recall** policy. Define the list using a semicolon to separate URIs. Make sure you include the URL scheme such as `http://`, `file://`, `https://www.`. Sites local to a supported browser like `edge://`, or `chrome://`, are filtered by default. For example: `https://www.Contoso.com;https://www.WoodgroveBank.com;https://www.Adatum.com`

> [!NOTE]
> - This setting applies only to Enterprise and Education editions of Windows.
> - Private browsing activity is filtered by default when using [supported web browsers](#supported-browsers). 
> - Be aware that websites are filtered when they are in the foreground or are in the currently opened tab of a supported browser. Parts of filtered websites can still appear in snapshots such as embedded content, the browser's history, or an opened tab that isn't in the foreground.
> - Filtering doesn't prevent browsers, internet service providers (ISPs), websites, organizations, or others from knowing that the website was accessed and building a history.
> - Changes to this policy take effect after device restart.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyUriListForRecall](mdm/policy-csp-windowsai.md#setdenyurilistforrecall) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyUriListForRecall](mdm/policy-csp-windowsai.md#setdenyurilistforrecall)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **>Set a list of URIs to be filtered from snapshots for Recall** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **>Set a list of URIs to be filtered from snapshots for Recall** |


**Set a list of apps to be filtered from snapshots for Recall** policy allows you to filter apps from being saved in snapshots. Define the list using a semicolon to separate apps. The list can include Application User Model IDs (AUMID) or the name of the executable file. For example: `code.exe;Microsoft. WindowsNotepad_8wekyb3d8bbwe!App;ms-teams.exe`

> [!Note]
> - This setting applies only to Enterprise and Education editions of Windows.
> - Like other Windows apps, such as the Snipping Tool, Recall won't store [digital rights management (DRM)](/windows/win32/wmformat/digital-rights-management-features) content. Recall doesn't record audio or save continuous video. It also doesn't save game video when Game Mode is active on platforms that support it.
> - Changes to this policy take effect after device restart.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyAppListForRecall](mdm/policy-csp-windowsai.md#setdenyapplistforrecall) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyAppListForRecall](mdm/policy-csp-windowsai.md#setdenyapplistforrecall)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Set a list of apps to be filtered from snapshots for Recall** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Set a list of apps to be filtered from snapshots for Recall**|


## Remote desktop connection clients filtered from snapshots

Snapshots won't be saved when remote desktop connection clients are used. The following remote desktop connection clients are filtered from snapshots:<!--9119193-->

   - [Remote Desktop Connection (mstsc.exe)](/windows-server/administration/windows-commands/mstsc)
   - [VMConnect.exe](/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) 
      - [Microsoft Remote Desktop from the Microsoft Store](/windows-server/remote/remote-desktop-services/clients/windows) is saved in snapshots. To prevent the app from being saved in snapshots, add it to the app filtering list.
   - [Azure Virtual Desktop (MSI)](/azure/virtual-desktop/users/connect-windows) 
      - [Azure Virtual Desktop apps from the Microsoft Store](/azure/virtual-desktop/users/connect-remote-desktop-client) are saved in snapshots. To prevent these apps from being saved in snapshots, add them to the app filtering list.
  - [Remote applications integrated locally (RAIL)](/openspecs/windows_protocols/ms-rdperp/485e6f6d-2401-4a9c-9330-46454f0c5aba) windows
  - [Windows App from the Microsoft Store](/windows-app/get-started-connect-devices-desktops-apps) is saved in snapshots. To prevent the app from being saved in snapshots, add it to the app filtering list.

If you're using a virtual desktop setup to protect your data, make sure you test that your supported clients honor screen capture protection. For example, both [Azure Virtual Desktop](/azure/virtual-desktop/overview) and [Windows 365](/windows-365/overview) have policies that you can set to prevent your content from being saved in a screenshot. For instance, there's screen capture protection in Azure Virtual Desktop. Check with the provider of your remote client software to see if they have a similar policy. For information about adding screen capture protection to a client, see the [Information for developers](#information-for-developers) section.

## Bring your own device (BYOD) considerations

For managed devices, IT admins have control over if they want to allow users access to Recall. It's removed by default unless IT sets the policy to enable Recall. When organizations allow users to BYOD, they need to consider the following:

- **Recall availability**: For unmanaged Copilot+ PC devices, Recall is available by default but a user has to opt in to save snapshots. Users can enable or disable Recall on their own. If multiple people sign in on a device with different accounts, each person needs to make the decision on if they would like to allow saving snapshots or not.

- **Conditional access restrictions**: On unmanaged devices, there isn't a way to determine if Recall is running and saving snapshots. Currently, there aren't any built-in [Conditional Access policies in Microsoft Intune](/mem/intune-service/protect/create-conditional-access-intune) or in [Microsoft Entra](/entra/identity/conditional-access/overview) for Recall. 

- **Security threat of screenshots**: Like numerous available applications for screen recording and snapshots, Recall uses general Windows screenshot APIs. It's a general security risk to allow screenshots of content that you want to prevent from being exfiltrated. Admins should ensure their sensitive content is protected from this type of risk. To help ensure your protected content stays protected, Recall will not store DRM content.

- **Recall and virtual machines**: If you're using a virtual desktop setup to protect your data, make sure you test that your supported clients honor screen capture protection. For example, both [Azure Virtual Desktop](/azure/virtual-desktop/overview) and [Windows 365](/windows-365/overview) have policies that you can set to prevent your content from being saved in a screenshot. For instance, there's [screen capture protection in Azure Virtual Desktop](/azure/virtual-desktop/screen-capture-protection). Check with the provider of your remote client software to see if they have a similar policy. For information about adding screen capture protection to a client, see the [Information for developers](#information-for-developers) section. 

- **Office content**: If Office content is only accessible inside the virtual desktop client, it can be protected from screen capture like all content on the virtual desktop. If Office content is accessible in the BYOD browser, you can try using protection with Purview, which is a Microsoft Data Loss Prevention tool. This allows you to create sensitivity classes that would prevent screenshots. You could, for example, set a policy such that all Office documents are excluded from screenshots. For more information, see [Protect Office documents with Microsoft Purview Information Protection](/deployedge/microsoft-edge-management-service-office-mip).


## Information for developers

If you're a developer and want to launch Recall, you can call the `ms-recall` protocol URI. When you call this URI, Recall opens and takes a snapshot of the screen, which is the default behavior for when Recall is launched. For more information about using Recall in your Windows app, see [Recall overview](/windows/ai/apis/recall) in the Windows AI API documentation.

If your remote desktop connection doesn't support screen capture protection, then it's an easy feature to add. Windows allows applications to exclude their window from being included in screenshot. This DRM flag is set by the application as a property on its window. It's a simple feature for application developers to implement using [SetWindowDisplayAffinity function (winuser.h)](/windows/win32/api/winuser/nf-winuser-setwindowdisplayaffinity). By setting the flag `WDA_EXCLUDEFROMCAPTURE`, the window content won't show up in Recall or any other screenshot application. 

## Microsoft's commitment to responsible AI

Microsoft has been on a responsible AI journey since 2017, when we defined our principles and approach to ensuring this technology is used in a way that is driven by ethical principles that put people first. For more about our responsible AI journey, the ethical principles that guide us, and the tooling and capabilities we've created to assure that we develop AI technology responsibly, see [Responsible AI](https://www.microsoft.com/ai/responsible-ai).

Recall's models use contextual cues in the entire image, including people or entities in the background, which is how the models can still associate the image with an individual, or describe emotions. Biometric data and inferencing are not used. Any processing that returns results that identify an individual or infer an individual's emotion is not the result of processing of the face, such as facial recognition, generation and comparison of facial templates, or other facial inferencing. For example, if an image contains a photo of a popular athlete wearing their team's jersey and their specific number, the models may still return a result that might identify the individual based on those contextual cues.

Recall can respond to questions related to perceived emotions of people in images. The processes underlying human emotion are complex, and there are cultural, geographical, and individual differences that influence how we may perceive, experience, and express emotions. Responses related to the emotions of people in images are based on how they appear and may not necessarily accurately indicate the internal state of individual people. 

Searches using terms for items or text that appear in an image yield more accurate results over searches using terms that don't directly appear in images but might be perceived about an image. Using distinctive terms rather than ambiguous terms also yield more accurate results.

Recall uses optical character recognition (OCR), local to the PC, to analyze snapshots and facilitate search. For more information about OCR, see [Transparency note and use cases for OCR](/legal/cognitive-services/computer-vision/ocr-transparency-note). For more information about privacy and security, see [Privacy and control over your Recall experience](https://support.microsoft.com/windows/privacy-and-control-over-your-recall-experience-d404f672-7647-41e5-886c-a3c59680af15).

## Providing feedback to Microsoft about Recall

If there's something you like, and especially if there's something you don't like about Recall you can submit feedback to Microsoft by selecting **…** then the Feedback icon in Recall. Filing feedback will send data from Recall to Microsoft, including any screenshots that a user attaches to the feedback.

## Related links

- [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai)
- [Manage Click to Do](manage-click-to-do.md)
- [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/)
- [Retrace your steps with Recall](https://support.microsoft.com/windows/aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c)
- [Privacy and control over your Recall experience](https://support.microsoft.com/windows/d404f672-7647-41e5-886c-a3c59680af15)
- [Click to Do in Recall](https://support.microsoft.com/topic/967304a8-32d1-4812-a904-fad59b5e6abf)
- [Previewing Recall with Click to Do on Copilot+ PCs with Windows Insiders in the Dev Channel](https://blogs.windows.com/windows-insider/2024/11/22/previewing-recall-with-click-to-do-on-copilot-pcs-with-windows-insiders-in-the-dev-channel/)
