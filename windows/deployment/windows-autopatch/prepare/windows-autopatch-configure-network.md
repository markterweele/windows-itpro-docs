---
title: Configure your network
description: This article details the network configurations needed for Windows Autopatch
ms.date: 03/31/2025
ms.service: windows-client
ms.subservice: autopatch
ms.topic: how-to
ms.localizationpriority: medium
author: tiaraquan
ms.author: tiaraquan
manager: bpardi
ms.reviewer: hathind
ms.collection:
  - tier2
---

# Configure your network

## Proxy configuration

### Proxy requirements

The proxy or firewall must support TLS 1.2. Otherwise, you might have to disable protocol detection.

### Required Microsoft product endpoints

There are URLs from several Microsoft products that must be in the allowed list so that Windows Autopatch devices can communicate with those Microsoft services. Use the links to see the complete list for each product.

| Microsoft service | URLs required on Allowlist |
| ----- | ----- |
| Microsoft Entra ID | [Hybrid identity required ports and protocols](/azure/active-directory/hybrid/reference-connect-ports)<p><p>[Active Directory and Active Directory Domain Services Port Requirements](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772723(v=ws.10))</p> |
| Microsoft Intune | [Intune network configuration requirements](/mem/intune/fundamentals/network-bandwidth-use)<p><p>[Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints)</p> |
| Windows Update client policies | [Windows Update client policies firewall and proxy requirements](https://support.microsoft.com/help/3084568/can-t-download-updates-from-windows-update-from-behind-a-firewall-or-p) |
| Windows 10/11 Enterprise including Windows Update client policies | [Manage connection endpoints for Windows 10 Enterprise, version 1909](/windows/privacy/manage-windows-1909-endpoints)<p><p>[Manage connection endpoints for Windows 10 Enterprise, version 2004](/windows/privacy/manage-windows-2004-endpoints)</p><p>[Connection endpoints for Windows 10 Enterprise, version 20H2](/windows/privacy/manage-windows-20h2-endpoints)</p><p>[Manage connection endpoints for Windows 10 Enterprise, version 21H1](/windows/privacy/manage-windows-21h1-endpoints)</p><p>[Manage connection endpoints for Windows 10 Enterprise, version 21H2](/windows/privacy/manage-windows-21h2-endpoints)</p><p>[Manage connection endpoints for Windows 11 Enterprise](/windows/privacy/manage-windows-11-endpoints)</p>|
| Microsoft 365 | [Microsoft 365 URL and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide&preserve-view=true) |
| Microsoft Edge | [Allowlist for Microsoft Edge Endpoints](/deployedge/microsoft-edge-security-endpoints) |
| Microsoft Teams | [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges) |

### Required Windows Autopatch endpoints for proxy and firewall rules

Windows Autopatch is a cloud service. There's a set of endpoints that Windows Autopatch services must be able to reach for the various aspects of the Windows Autopatch service.

You can optimize your network by sending all trusted Microsoft 365 network requests directly through your firewall or proxy to bypass authentication, and all additional packet-level inspection or processing. This process reduces latency and your perimeter capacity requirements.

The following URLs must be on the allowed list of your proxy and firewall so that Windows Autopatch devices can communicate with Microsoft services. The Windows Autopatch URL is used for anything our service runs on the customer API. You must ensure this URL is always accessible on your corporate network

| Microsoft service | URLs required on allowlist |
| ----- | ----- |
| Windows Autopatch | <ul><li>mmdcustomer.microsoft.com</li><li>mmdls.microsoft.com</li><li>devicelistenerprod.microsoft.com (devicelistenprod.eudb.microsoft.com for tenants with billing addresses in the [EU Data Boundary](/privacy/eudb/eu-data-boundary-learn#eu-data-boundary-countries-and-datacenter-locations))</li><li>login.windows.net</li><li>device.autopatch.microsoft.com</li><li>services.autopatch.microsoft.com</li><li>payloadprod*.blob.core.windows.net</li><li>*.webpubsub.azure.com</li></ul>|

## Delivery Optimization

Delivery Optimization is a peer-to-peer distribution technology available in Windows 10 and Windows 11 that allows devices to share content, such as updates, that the devices downloaded from Microsoft over the internet. Delivery Optimization can help reduce network bandwidth because the device can get portions of the update from another device on the same local network instead of having to download the update completely from Microsoft.

For more information, see [What is Delivery Optimization?](/windows/deployment/do/waas-delivery-optimization)
