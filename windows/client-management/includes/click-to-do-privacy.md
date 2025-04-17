---
author: mestew
ms.author: mstewart
ms.topic: include
ms.date: 04/25/2025
---
<!-- this include file is used in the following articles: manage-recall.md & manage-click-to-do.md. Headings are driven by the articles' context -->

When you choose to send info from Click to Do to an app, like Paint, Click to Do will temporarily save this info in order to complete the transfer. Click to Do creates a temporary file in the following location: 

- `C:\Users\{username}\AppData\Local\Temp`

Temporary files may also be saved when you choose send feedback. These temporary files aren't saved long term. Click to Do doesn't keep any content from your screen after completing the requested action, but some [diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization) is gathered to keep Click to Do secure, up to date, and working.

Click to Do's more intelligent text actions, including **Summarize**, **Rewrite (Casual)**, **Rewrite (Formal)**,**Rewrite (Refine)**, and **Create a bulleted list** are powered by a state-of-the-art small language model called Phi Silica. Phi Silica leverages the NPU and the language model runs locally on Copilot+ PCs. Phi Silica ships inbox with Windows on Copilot+ PCs. 

When a user clicks on the Click to Do text actions, the selected text and the chosen action are sent to Phi Silica as part of a prompt. Phi Silica intelligently rewrites the selected text as per the user's request and streams back the response from the model. Phi Silica provides responses quickly and efficiently, using little power. For more information, see [Phi Silica, small but mighty on-device SLM](https://blogs.windows.com/windowsexperience/?p=179250). 

In keeping with Microsoft's commitment to data privacy and security, all saved images and processed data are kept on the device and processed locally. However, Click to Do allows you to choose if you want to get more information about your selected content online. When you choose one of the following Click to Do actions, the selected content is sent to the online provider from your local device to complete your request:

- **Search the web**: Sends the selected content to Bing using Microsoft Edge
- **Open website**: Opens the selected website in your default browser
-	**Visual search with Bing**: Sends the selected content to [Bing visual search](https://support.microsoft.com/topic/62771a0c-4daa-47e4-a9f7-e1bfa85f0d7c) using your default browser