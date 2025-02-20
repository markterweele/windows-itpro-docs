---
title: Manage Click to Do for Windows clients
description: Learn how to manage Click to Do for commercial environments and about Click to Do features.
ms.topic: how-to
ms.subservice: windows-copilot
ms.date: 03/01/2025
ms.author: mstewart
author: mestew
ms.collection:
  - windows-copilot
  - magic-ai-copilot
appliesto:
- ✅ <a href="https://www.microsoft.com/windows/business/devices/copilot-plus-pcs#copilot-plus-pcs" target="_blank">Copilot+ PCs</a>
---

# Manage Click to Do
<!--9687427-->
>**Looking for consumer information?** See [Click to Do: do more with what's on your screen](https://support.microsoft.com/topic/6848b7d5-7fb0-4c43-b08a-443d6d3f5955).

Click to Do (preview) helps users to get things done faster by identifying text and images on their screen that they can take actions with. This article provides information about Click to Do and how to manage it in a commercial environment.

> [!NOTE]
> - Click to Do is now available in preview to Copilot+ PCs through the Windows Insider Program. For more information, see [Placeholder Blog](https://blogs.windows.com/windows-insider/2024/12/06/previewing-more-copilot-experiences-with-windows-insiders-in-the-dev-channel/).
> - In-market commercial devices are defined as devices with an Enterprise (ENT) or Education (EDU) SKU or any premium SKU device that is managed by an IT administrator (whether via Microsoft Endpoint Manager or other endpoint management solution), has a volume license key, or is joined to a domain. Commercial devices during Out of Box Experience (OOBE) are defined as those with ENT or EDU SKU or any premium SKU device that has a volume license key or is Microsoft Entra joined. 
> - Click to Do is optimized for select languages English, Chinese (simplified), French, German, Japanese, and Spanish. Content-based and storage limitations apply. For more information, see [https://aka.ms/copilotpluspcs](https://aka.ms/copilotpluspcs).

## ## What is Click to Do?

Click to Do (preview) analyzes what's on the screen and then allows users to choose the text or image they want to take action on. 

The analysis of screenshots is always performed locally on the device. Analysis only begins after users actively engage with Click to Do and ends when they exit Click to Do. Click to Do only identifies text and images, not the content of those text or images. It doesn't analyze any content in, for example, minimized applications that are not on the screen.  
 
Content is only shared if users choose to complete an action like **Search the web**. When Click to Do is active, the cursor is blue and white. The cursor also changes shape depending on the type of info beneath it. What users can do with the info changes based on what kind of content Click to Do detects.


## System requirements

Click to Do has the following minimum requirements:

- A [Copilot+ PC](https://aka.ms/copilotpluspcs)
  - The more intelligent text actions are available only on Snapdragon-powered Copilot+ PCs today when your language is set to English with support for AMD and Intel-powered Copilot+ PCs coming soon. 


## Configure policy for Click to Do

Click to Do lets people take action on content on their screens. When activated, it takes a screenshot of their screen and analyzes it to present actions. Click to Do ends when they exit it, and it can't take screenshots while closed. Screenshot analysis is always performed locally on their device. By default, Click to Do is enabled for users.

This policy setting allows you to determine whether Click to Do is available for users on their device.

When the policy is enabled, the Click to Do component and entry points will not be available to users.

When the policy is disabled, users will have Click to Do available on their device.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[DisableClickToDo](mdm/policy-csp-windowsai.md#DisableClickToDo) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[DisableClickToDo](mdm/policy-csp-windowsai.md#DisableClickToDo)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Disable Click to Do** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Disable Click to Do**|

