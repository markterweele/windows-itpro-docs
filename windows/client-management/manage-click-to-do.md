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

Click to Do (preview) helps users to get things done faster by identifying text and images that are currently on their screen so they can perform actions on them. This article provides information about Click to Do and how to manage it in a commercial environment.

> [!NOTE]
> - Click to Do is now available in preview to Copilot+ PCs through the Windows Insider Program. For more information, see [Placeholder Blog](https://blogs.windows.com/windows-insider/2024/12/06/previewing-more-copilot-experiences-with-windows-insiders-in-the-dev-channel/).
> - In-market commercial devices are defined as devices with an Enterprise (ENT) or Education (EDU) SKU or any premium SKU device that is managed by an IT administrator (whether via Microsoft Endpoint Manager or other endpoint management solution), has a volume license key, or is joined to a domain. Commercial devices during Out of Box Experience (OOBE) are defined as those with ENT or EDU SKU or any premium SKU device that has a volume license key or is Microsoft Entra joined. 
> - Click to Do is optimized for select languages English, Chinese (simplified), French, German, Japanese, and Spanish. Content-based and storage limitations apply. For more information, see [https://aka.ms/copilotpluspcs](https://aka.ms/copilotpluspcs).

## ## What is Click to Do?

Click to Do (preview) analyzes what's on the screen and then allows users to choose the text or image they want to take action on. 

The analysis of screenshots is always performed locally on the device. Analysis only begins after users actively engage with Click to Do and ends when they exit Click to Do. Click to Do only identifies text and images, not the content of those text or images. It doesn't analyze any content in, for example, minimized applications that aren't on the screen.  
 
Content is only shared if users choose to complete an action like **Search the web**. When Click to Do is active, the cursor is blue and white. The cursor also changes shape depending on the type of info beneath it. What users can do with the info changes based on what kind of content Click to Do detects. For instance, users can perform actions on text such as copy, summarize or rewrite it, or share it. For images, users can perform actions such as copy, save, or blurring the background using Microsoft Photos.

:::image type="content" source="images/9687427-text-actions-click-to-do.png" alt-text="Screenshot of the text actions in Click to Do" lightbox="images/9687427-text-actions-click-to-do.png":::


## System requirements

Click to Do has the following minimum requirements:

- A [Copilot+ PC](https://aka.ms/copilotpluspcs)
  - The more intelligent text actions are available only on Snapdragon-powered Copilot+ PCs today when your language is set to English with support for AMD and Intel-powered Copilot+ PCs coming soon. 


## Configure policy for Click to Do

Click to Do lets people take action on content that's currently on their screens. When activated, it takes a screenshot of their screen and analyzes it to present actions. Click to Do ends when they exit it, and it can't take screenshots while closed. Screenshot analysis is always performed locally on the device. By default, Click to Do is enabled for users.

This policy setting allows you to determine whether Click to Do is available for users on their device.

When the policy is enabled, the Click to Do component and entry points will not be available to users.

When the policy is disabled, users will have Click to Do available on their device.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[DisableClickToDo](mdm/policy-csp-windowsai.md#DisableClickToDo) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[DisableClickToDo](mdm/policy-csp-windowsai.md#DisableClickToDo)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Disable Click to Do** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Disable Click to Do**|

## Click to Do privacy considerations  

When you choose to send info from Click to Do to an app, like Paint, Click to Do will temporarily save this info in order to complete the transfer. Click to Do creates a temporary file in the following location: 

- `C:\Users\{username}\AppData\Local\Temp`

Temporary files may also be saved when you choose send feedback. These temporary files aren't saved long term. Click to Do doesn't keep any content from your screen after completing the requested action, but some [diagnostic data](..\privacy\configure-windows-diagnostic-data-in-your-organization.md) is gathered to keep Click to Do secure, up to date, and working.

Click to Do's more intelligent text actions, including **Summarize**, **Rewrite (Casual)**, **Rewrite (Formal)**, and **Refine**, are powered by a state-of-the-art small language model called Phi Silica. Phi Silica leverages the NPU and the language model runs locally on Copilot+ PCs. Phi Silica ships inbox with Windows on Copilot+ PCs. 

When a user clicks on the Click to Do text actions, the selected text and the chosen action are sent to Phi Silica as part of a prompt. Phi Silica intelligently rewrites the selected text as per the user's request and streams back the response from the model. Phi Silica provides responses quickly and efficiently, using very little power. For more information, see [Phi Silica, small but mighty on-device SLM](https://blogs.windows.com/windowsexperience/?p=179250). 

While Phi Silica runs locally, Click to Do's more intelligent text actions also leverage the power of Microsoft's secure cloud to improve your text results by ensuring prompts and responses are safe and appropriate. When a text action is selected, the highlighted text is sent to Microsoft's secure cloud to perform this check. This data is automatically deleted once this check is completed. For more information about privacy for Click to Do, see the [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=521839%E2%80%AF).

## Microsoft's commitment to responsible AI and Privacy
 
Microsoft has been working to advance AI responsibly since 2017, when we first defined our AI principles and later operationalized our approach through our Responsible AI Standard. Privacy and security are core principles as we develop and deploy AI systems. We work to help our customers use our AI products responsibly, sharing our learnings, and building trust-based partnerships. For more about our responsible AI efforts, the principles that guide us, and the tools and capabilities we've created to assure that we develop AI technology responsibly, see [Responsible AI](https://www.microsoft.com/ai/responsible-ai).


Click to Do uses optical character recognition (OCR) on your PC to detect text entities on screenshots. For more information about OCR, see [Transparency note and use cases for OCR](/legal/cognitive-services/computer-vision/ocr-transparency-note). 

Click to Do's intelligent text actions use a small language model called Phi Silica. For more information on Phi Silica, see [Get started with Phi Silica in the Windows App SDK](/windows/ai/apis/phi-silica#responsible-ai). For information on the Responsible AI principles guiding Phi Silica deployment and the safety measures in place when using generative language models, please see [Responsible Generative AI Development on Windows](/windows/ai/rai). 


Click to Do's models have undergone fairness assessments, alongside comprehensive responsible AI, security and privacy assessments, to make sure the technology is effective and equitable while adhering to Microsoft's Responsible AI best practices.

## Related links

- [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai)
- [Responsible AI](https://www.microsoft.com/ai/responsible-ai)