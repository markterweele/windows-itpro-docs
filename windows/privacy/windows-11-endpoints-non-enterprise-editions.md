---
title: Windows 11 connection endpoints for non-Enterprise editions
description: Explains what Windows 11 endpoints are used in non-Enterprise editions. Specific to Windows 11.
ms.service: windows-client
ms.subservice: itpro-privacy
ms.localizationpriority: high
author: DHB-MSFT
ms.author: danbrown
manager: dansimp
ms.date: 05/23/2025 
ms.topic: reference
hideEdit: true 
ms.collection: 
- privacy-windows
- must-keep
---
# Windows 11 connection endpoints for non-Enterprise editions

 **Applies to**

- Windows 11

In addition to the endpoints listed for [Windows 11 Enterprise](manage-windows-11-endpoints.md), the following endpoints are available on other non-Enterprise editions of Windows 11.

The following methodology was used to derive the network endpoints:

1. Set up the latest version of Windows 11 on a test virtual machine using the default settings.
2. Leave the device(s) running idle for a week ("idle" means a user isn't interacting with the system/device).
3. Use globally accepted network protocol analyzer/capturing tools and log all background egress traffic.
4. Compile reports on traffic going to public IP addresses.
5. The test virtual machine(s) was logged into using a local account, and wasn't joined to a domain or Microsoft Entra ID.
6. All traffic was captured in our lab using an IPV4 network. Therefore, no IPV6 traffic is reported here.
7. These tests were conducted in an approved Microsoft lab. It's possible your results may be different.
8. These tests were conducted for one week. If you capture traffic for longer, you may have different results.

> [!NOTE]
> Microsoft uses global load balancers that can appear in network trace-routes. For example, an endpoint for *.akadns.net might be used to load balance requests to an Azure datacenter, which can change over time.

## Windows 11 Home

| **Area** | **Description** | **Protocol** | **Destination** |
|-----------|--------------- |------------- |-----------------|
| Activity Feed Service |The following endpoints are used by Activity Feed Service, which enables multiple cross-device data roaming scenarios on Windows|TLSv1.2/HTTPS/HTTP|activity.windows.com|
|Apps|The following endpoints are used for the Weather app.|TLSv1.2/HTTPS/HTTP|tile-service.weather.microsoft.com|
||The following endpoint is used by the Photos app to download configuration files, and to connect to the Office 365 portal's shared infrastructure, including Office in a browser.|TLSv1.2/HTTPS/HTTP|evoke-windowsservices-tas.msedge.net|
||The following endpoint is used for OneNote Live Tile.|HTTPS/HTTP|cdn.onenote.net|
||Used for Spotify Live Tile|HTTPS/HTTP|spclient.wg.spotify.com|
|Certificates|The following endpoint is used by the Automatic Root Certificates Update component to automatically check the list of trusted authorities on Windows Update to see if an update is available.|TLSv1.2/HTTPS/HTTP|ctldl.windowsupdate.com/*|
|Cortana and Live Tiles|The following endpoints are related to Cortana and Live Tiles|TLSv1.2/HTTPS/HTTP|www.bing.com*|
|||HTTPS/HTTP|fp.msedge.net|
|||HTTPS/HTTP|k-ring.msedge.net|
|||TLSv1.2|b-ring.msedge.net|
|Device authentication|The following endpoint is used to authenticate a device.|HTTPS|login.live.com*|
|Device Directory Service|Used by Device Directory Service to keep track of user-device associations and storing metadata about the devices.|HTTPS/HTTP|cs.dds.microsoft.com|
|Device metadata|The following endpoint is used to retrieve device metadata.|TLSv1.2/HTTP|dmd.metaservices.microsoft.com|
|Diagnostic data|The following endpoints are used by the Connected User Experiences and Telemetry component and connects to the Microsoft Data Management service. <br/>If you turn off traffic for this endpoint, diagnostic and usage information, which helps Microsoft find and fix problems and improve our products and services, won't be sent back to Microsoft.|TLSv1.2/HTTP|v10.events.data.microsoft.com|
||The following endpoints are used by Windows Error Reporting.|TLSv1.2/HTTPS/HTTP|watson.telemetry.microsoft.com|
|Font Streaming|The following endpoints are used to download fonts on demand.|TLSv1.2/HTTPS|fs.microsoft.com*|
|Licensing|The following endpoint is used for online activation and some app licensing.|HTTPS/HTTP|*licensing.mp.microsoft.com|
|||HTTPS|licensing.mp.microsoft.com/v7.0/licenses/content|
|Location|The following endpoints are used for location data.|TLSV1.2|inference.location.live.net|
|Maps|The following endpoints are used to check for updates to maps that have been downloaded for offline use.|HTTPS/HTTP|maps.windows.com| 
|||HTTPS/HTTP|*.ssl.ak.dynamic.tiles.virtualearth.net|
|||HTTPS/HTTP|*.ssl.ak.tiles.virtualearth.net|
|||HTTPS/HTTP|dev.virtualearth.net|
|||HTTPS/HTTP|ecn.dev.virtualearth.net|
|||HTTPS/HTTP|ssl.bing.com|
|Microsoft Account|The following endpoints are used for Microsoft accounts to sign in|TLSv1.2/HTTPS/HTTP|*login.live.com|
|Microsoft Edge| This network traffic is related to the Microsoft Edge browser. The Microsoft Edge browser requires these endpoints to contact external websites.|HTTPS/HTTP|edge.activity.windows.com </br> edge.microsoft.com|
|Microsoft Edge|The following endpoint is used by Microsoft Edge Update service to check for new updates. If you disable this endpoint, Microsoft Edge won’t be able to check for and apply new edge updates.|HTTPS/HTTP|msedge.api.cdp.microsoft.com|
|Microsoft Store|The following endpoint is used to download image files that are called when applications run (Microsoft Store or Inbox MSN Apps)|TLSv1.2/HTTPS/HTTP|img-prod-cms-rt-microsoft-com.akamaized.net|
||The following endpoint is used for the Windows Push Notification Services (WNS). WNS enables third-party developers to send toast, tile, badge, and raw updates from their own cloud service. This provides a mechanism to deliver new updates to your users in a power-efficient and dependable way.|TLSv1.2/HTTPS|*.wns.windows.com|
||The following endpoint is used to revoke licenses for malicious apps in the Microsoft Store.|TLSv1.2/HTTPS/HTTP|storecatalogrevocation.storequality.microsoft.com|
||The following endpoints are used to communicate with Microsoft Store.|TLSv1.2/HTTPS/HTTP|*displaycatalog.mp.microsoft.com|
|||HTTPS|storesdk.dsx.mp.microsoft.com|
||The following endpoint is used to get Microsoft Store analytics.|TLSv1.2/HTTPS/HTTP|manage.devcenter.microsoft.com|
||The following endpoints are used get images that are used for Microsoft Store suggestions|TLSv1.2|store-images.s-microsoft.com|
|Network Connection Status Indicator (NCSI)|Network Connection Status Indicator (NCSI) detects Internet connectivity and corporate network connectivity status. NCSI sends a DNS request and HTTP query to this endpoint to determine if the device can communicate with the Internet.|TLSv1.2/HTTP|www.msftconnecttest.com*|
|Office|The following endpoints are used to connect to the Office 365 portal's shared infrastructure, including Office in a browser.|TLSv1.2/HTTPS/HTTP|outlook.office365.com|
|||TLSv1.2/HTTPS|office.com|
|||TLSv1.2/HTTPS|blobs.officehome.msocdn.com|
|||HTTPS/HTTP|officehomeblobs.blob.core.windows.net|
|||HTTPS/HTTP|*.blob.core.windows.net|
|||TLSv1.2|self.events.data.microsoft.com|
|||HTTPS/HTTP|outlookmobile-office365-tas.msedge.net|
|||HTTP|roaming.officeapps.live.com|
|||HTTPS/HTTP|substrate.office.com|
|OneDrive|The following endpoints are related to OneDrive.|HTTPS|g.live.com|
|||TLSv1.2/HTTPS|oneclient.sfx.ms|
|||HTTPS/TLSv1.2|logincdn.msauth.net|
|||HTTPS/HTTP|windows.policies.live.net|
|||HTTPS/HTTP|api.onedrive.com|
|||HTTPS/HTTP|skydrivesync.policies.live.net|
|||HTTPS/HTTP|*storage.live.com|
|||HTTPS/HTTP|*settings.live.net|
|Settings|The following endpoint is used as a way for apps to dynamically update their configuration. Apps such as System Initiated User Feedback and the Xbox app use it.|TLSv1.2/HTTPS/HTTP|settings.data.microsoft.com*|
|||TLSv1.2/HTTPS/HTTP|settings-win.data.microsoft.com*|
|Skype|The following endpoint is used to retrieve Skype configuration values.|TLSv1.2/HTTPS/HTTP|*.pipe.aria.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|config.edge.skype.com|
|Teams|The following endpoint is used for Microsoft Teams application.|TLSv1.2/HTTPS/HTTP|config.teams.microsoft.com|
|Microsoft Defender Antivirus|The following endpoints are used for Windows Defender when Cloud-based Protection is enabled|TLSv1.2/HTTPS|wdcp.microsoft.com </br>wdcpalt.microsoft.com|
|||HTTPS/HTTP|*.smartscreen-prod.microsoft.com|
|||TLSv1.2|definitionupdates.microsoft.com|
||The following endpoints are used for Windows Defender SmartScreen reporting and notifications.|TLSv1.2|*.smartscreen.microsoft.com|
|||TLSv1.2/HTTP|checkappexec.microsoft.com|
|Windows Spotlight|The following endpoints are used to retrieve Windows Spotlight metadata that describes content, such as references to image locations, as well as suggested apps, Microsoft account notifications, and Windows tips.|TLSv1.2/HTTPS/HTTP|arc.msn.com*</br>ris.api.iris.microsoft.com|
|||HTTPS|mucp.api.account.microsoft.com|
|Windows Update|The following endpoint is used for Windows Update downloads of apps and OS updates, including HTTP downloads or HTTP downloads blended with peers.|TLSv1.2/HTTPS/HTTP|*.prod.do.dsp.mp.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|*.dl.delivery.mp.microsoft.com|
||The following endpoints are used to download operating system patches, updates, and apps from Microsoft Store.|TLSv1.2/HTTP|*.windowsupdate.com|
|||TLSv1.2/HTTPS/HTTP|*.delivery.mp.microsoft.com|
||The following endpoints enable connections to Windows Update, Microsoft Update, and the online services of the Store to help keep the device secure.|TLSv1.2/HTTPS/HTTP|*.update.microsoft.com|
||The following endpoint is used for compatibility database updates for Windows.|HTTPS/HTTP|adl.windows.com|
||The following endpoint is used for content regulation.|TLSv1.2/HTTPS/HTTP|tsfe.trafficshaping.dsp.mp.microsoft.com|
|Xbox Live|The following endpoints are used for Xbox Live.|TLSv1.2/HTTPS/HTTP|dlassets-ssl.xboxlive.com|
|||TLSv1.2/HTTPS|da.xboxservices.com|
|||HTTPS|www.xboxab.com|


## Windows 11 Pro

| **Area** | **Description** | **Protocol** | **Destination** |
| --- | --- | --- | ---|
| Activity Feed Service |The following endpoints are used by Activity Feed Service, which enables multiple cross-device data roaming scenarios on Windows|TLSv1.2/HTTPS/HTTP|activity.windows.com|
|||HTTP|assets.activity.windows.com|
|Apps|The following endpoint is used for the Weather app.|TLSv1.2/HTTPS/HTTP|tile-service.weather.microsoft.com|
||The following endpoint is used by the Photos app to download configuration files, and to connect to the Office 365 portal's shared infrastructure, including Office in a browser.|TLSv1.2/HTTPS/HTTP|evoke-windowsservices-tas.msedge.net|
||The following endpoint is used for OneNote Live Tile.|HTTPS/HTTP|cdn.onenote.net|
||The following endpoint is used for Spotify Live Tile.|HTTPS/HTTP|spclient.wg.spotify.com|
|Certificates|The following endpoints are used by the Automatic Root Certificates Update component to automatically check the list of trusted authorities on Windows Update to see if an update is available.|TLSv1.2/HTTPS/HTTP|ctldl.windowsupdate.com/*|
|||HTTP|ocsp.digicert.com|
|Cortana and Live Tiles|The following endpoints are related to Cortana and Live Tiles|TLSv1.2/HTTPS/HTTP|www.bing.com*|
|||HTTPS|business.bing.com|
|||HTTP|c.bing.com|
|||HTTP|edgeassetservice.azureedge.net|
|||HTTP|fp.msedge.net|
|||HTTP|fp-vs.azureedge.net|
|||TLSv1.2|ln-ring.msedge.net|
|||TLSv1.2|prod-azurecdn-akamai-iris.azureedge.net|
|||HTTP|r.bing.com|
|||TLSv1.2/HTTP|s-ring.msedge.net|
|||HTTP|t-ring.msedge.net|
|||HTTP|t-ring-fdv2.msedge.net|
|||TLSv1.2|tse1.mm.bing.net|
|||TLSv1.2|widgetcdn.azureedge.net|
|||TLSv1.2|widgetservice.azurefd.net|
|Device authentication|The following endpoint is used to authenticate a device.|HTTPS|login.live.com*|
|Device metadata|The following endpoint is used to retrieve device metadata.|TLSv1.2/HTTP|dmd.metaservices.microsoft.com|
|Diagnostic data||HTTP|browser.events.data.msn.com|
|||TLSv1.2|functional.events.data.microsoft.com|
|||TLSv1.2/HTTP|www.microsoft.com|
||The following endpoints are used by the Connected User Experiences and Telemetry component and connects to the Microsoft Data Management service. <br/>If you turn off traffic for this endpoint, diagnostic and usage information, which helps Microsoft find and fix problems and improve our products and services, won't be sent back to Microsoft. |TLSv1.2/HTTP|v10.events.data.microsoft.com|
|||TLSv1.2/HTTP|self.events.data.microsoft.com|
||The following endpoints are used by Windows Error Reporting.|TLSv1.2/HTTPS/HTTP|watson.telemetry.microsoft.com|
|||TLSv1.2/HTTP|watson.events.data.microsoft.com|
|Font Streaming|The following endpoints is used to download fonts on demand.|TLSv1.2/HTTPS|fs.microsoft.com*|
|Licensing|The following endpoint is used for online activation and some app licensing.|TLSv1.2/HTTPS/HTTP|*licensing.mp.microsoft.com|
|Location|The following endpoint is used for location data. If you turn off traffic for this endpoint, apps can't use location data.|TLSv1.2|inference.location.live.net|
|Maps|The following endpoints are used to check for updates to maps that have been downloaded for offline use.|HTTPS/HTTP|maps.windows.com|
|||HTTP|ecn-us.dev.virtualearth.net|
|Microsoft Account|The following endpoint is used for Microsoft accounts to sign in. |TLSv1.2/HTTPS/HTTP|*login.live.com|
|Microsoft Defender Antivirus|The following endpoints are used for Windows Defender when Cloud-based Protection is enabled|TLSv1.2/HTTPS|wdcp.microsoft.com|
|||TLSv1.2/HTTPS|wdcpalt.microsoft.com|
||The following endpoints are used for Windows Defender SmartScreen reporting and notifications.|HTTPS/HTTP|*.smartscreen-prod.microsoft.com|
|||TLSv1.2|*.smartscreen.microsoft.com|
|||TLSv1.2/HTTP|checkappexec.microsoft.com|
|Microsoft Edge|The following endpoints are used by Microsoft Edge Update service to check for new updates. If you disable this endpoint, Microsoft Edge won’t be able to check for and apply new edge updates. |HTTPS/HTTP|msedge.api.cdp.microsoft.com|
|||TLSv1.2/HTTP|edge.microsoft.com|
|||HTTP|edge.nelreports.net|
|||TLSv1.2/HTTP|windows.msn.com|
|Microsoft Store|The following endpoints are used to download image files that are called when applications run (Microsoft Store or Inbox MSN Apps)|TLSv1.2/HTTPS/HTTP|img-prod-cms-rt-microsoft-com.akamaized.net|
|||HTTP|img-s-msn-com.akamaized.net|
||The following endpoint is used for the Windows Push Notification Services (WNS). WNS enables third-party developers to send toast, tile, badge, and raw updates from their own cloud service. This provides a mechanism to deliver new updates to your users in a power-efficient and dependable way.|TLSv1.2/HTTPS|*.wns.windows.com|
||The following endpoint is used to revoke licenses for malicious apps in the Microsoft Store.|TLSv1.2/HTTPS/HTTP|storecatalogrevocation.storequality.microsoft.com|
||The following endpoints are used to communicate with Microsoft Store.|TLSv1.2/HTTPS/HTTP|*displaycatalog.mp.microsoft.com|
|||HTTPS|storesdk.dsx.mp.microsoft.com|
||The following endpoint is used to get Microsoft Store analytics.|TLSv1.2/HTTPS/HTTP|manage.devcenter.microsoft.com|
||The following endpoint is needed to load the content in the Microsoft Store app.|HTTP|storeedgefd.dsx.mp.microsoft.com|
|Microsoft To Do|The following endpoints are used for the Microsoft To Do app.|HTTP|staging.to-do.microsoft.com|
|||TLSv1.2/HTTP|to-do.microsoft.com|
|Network Connection Status Indicator (NCSI)|Network Connection Status Indicator (NCSI) detects Internet connectivity and corporate network connectivity status. NCSI sends a DNS request and HTTP query to this endpoint to determine if the device can communicate with the Internet.|TLSv1.2/HTTP|www.msftconnecttest.com*|
|||HTTP|ipv6.msftconnecttest.com|
|Office|The following endpoints are used to connect to the Office 365 portal's shared infrastructure, including Office in a browser.|TLSv1.2/HTTPS|blobs.officehome.msocdn.com|
|||TLSv1.2/HTTPS/HTTP|*.blob.core.windows.net|
|||TLSv1.2/HTTP|ecs.nel.measure.office.net|
|||TLSv1.2/HTTP|ocws.officeapps.live.com|
|||TLSv1.2/HTTP|odc.officeapps.live.com|
|||TLSv1.2/HTTPS|office.com|
|||TLSv1.2/HTTPS/HTTP|officeclient.microsoft.com|
|||HTTPS/HTTP|officehomeblobs.blob.core.windows.net|
|||TLSv1.2/HTTPS/HTTP|outlook.office365.com|
|||HTTPS/HTTP|outlookmobile-office365-tas.msedge.net|
|||HTTP|roaming.officeapps.live.com|
|||TLSv1.2|self.events.data.microsoft.com|
|||HTTPS/HTTP|substrate.office.com|
|||HTTP|tfl.nel.measure.office.net|
|OneDrive|The following endpoints are related to OneDrive.|HTTP|ams03pap005.storage.live.com|
|||HTTP|api.onedrive.com|
|||HTTPS|g.live.com|
|||HTTPS/TLSv1.2|logincdn.msauth.net|
|||TLSv1.2/HTTPS|oneclient.sfx.ms|
|||HTTP|onedrive.live.com|
|||HTTP|sat02pap005.storage.live.com|
|||HTTPS/HTTP|*settings.live.net|
|||HTTP|skyapi.live.net|
|||HTTP|skydrivesync.policies.live.net|
|||HTTPS/HTTP|*storage.live.com|
|||HTTPS/HTTP|windows.policies.live.net|
|Settings|The following endpoints are used as a way for apps to dynamically update their configuration. Apps such as System Initiated User Feedback and the Xbox app use it.|TLSv1.2/HTTPS/HTTP|settings.data.microsoft.com*|
|||TLSv1.2/HTTPS/HTTP|settings-win.data.microsoft.com*|
|Skype|The following endpoints are used to retrieve Skype configuration values.|TLSv1.2/HTTPS/HTTP|*.pipe.aria.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|config.edge.skype.com|
|||HTTP|edge.skype.com|
|||HTTP|experimental-api.asm.skype.com|
|||HTTP|trouter-azsc-ukwe-0-b.trouter.skype.com|
|||HTTP|us-api.asm.skype.com|
|Teams|The following endpoints are used for Microsoft Teams application.|TLSv1.2/HTTPS/HTTP|config.teams.microsoft.com|
|||TLSv1.2/HTTP|teams.events.data.microsoft.com|
|||HTTP|teams.live.com|
|||HTTP|statics.teams.cdn.live.net|
|||HTTP|statics.teams.cdn.office.net|
|Windows Spotlight|The following endpoints are used to retrieve Windows Spotlight metadata that describes content, such as references to image locations, as well as suggested apps, Microsoft account notifications, and Windows tips.|TLSv1.2/HTTP|api.msn.com|
|||TLSv1.2/HTTPS/HTTP|arc.msn.com|
|||TLSv1.2/HTTP|assets.msn.com|
|||HTTP|c.msn.com|
|||TLSv1.2/HTTP|fd.api.iris.microsoft.com|
|||HTTP|ntp.msn.com|
|||TLSv1.2/HTTPS/HTTP|ris.api.iris.microsoft.com|
|||HTTP|srtb.msn.com|
|||TLSv1.2/HTTP|www.msn.com|
|Windows Update||TLSv1.2|definitionupdates.microsoft.com|
||The following endpoints are used for Windows Update downloads of apps and OS updates, including HTTP downloads or HTTP downloads blended with peers.|TLSv1.2/HTTPS/HTTP|*.prod.do.dsp.mp.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|*.dl.delivery.mp.microsoft.com|
||The following endpoints are used to download operating system patches, updates, and apps from Microsoft Store.|TLSv1.2/HTTP|*.windowsupdate.com|
|||TLSv1.2/HTTPS/HTTP|*.delivery.mp.microsoft.com|
||The following endpoint enables connections to Windows Update, Microsoft Update, and the online services of the Store to help keep the device secure.|TLSv1.2/HTTPS/HTTP|*.update.microsoft.com|
||The following endpoint is used for compatibility database updates for Windows.|HTTPS/HTTP|adl.windows.com|
||The following endpoint is used for content regulation.|TLSv1.2/HTTPS/HTTP|tsfe.trafficshaping.dsp.mp.microsoft.com|
|Xbox Live|The following endpoints are used for Xbox Live.|TLSv1.2/HTTPS/HTTP|dlassets-ssl.xboxlive.com|
|||TLSv1.2/HTTPS|da.xboxservices.com|




## Windows 11 Education

| **Area** | **Description** | **Protocol** | **Destination** |
| --- | --- | --- | ---|
| Activity Feed Service |The following endpoints are used by Activity Feed Service, which enables multiple cross-device data roaming scenarios on Windows|TLSv1.2/HTTPS/HTTP|activity.windows.com|
|Apps|The following endpoints are used for the Weather app.|TLSv1.2/HTTPS/HTTP|tile-service.weather.microsoft.com|
||The following endpoint is used by the Photos app to download configuration files, and to connect to the Office 365 portal's shared infrastructure, including Office in a browser.|TLSv1.2/HTTPS/HTTP|evoke-windowsservices-tas.msedge.net|
||The following endpoint is used for OneNote Live Tile.|HTTPS/HTTP|cdn.onenote.net|
|Bing Search|The following endpoint is used by Microsoft Search in Bing enabling users to search across files, SharePoint sites, OneDrive content, Teams and Viva Engage conversations, and other shared data sources in an organization, as well as the web.|HTTPS|business.bing.com|
|Certificates|The following endpoint is used by the Automatic Root Certificates Update component to automatically check the list of trusted authorities on Windows Update to see if an update is available.|TLSv1.2/HTTPS/HTTP|ctldl.windowsupdate.com/*|
|Cortana and Live Tiles|The following endpoints are related to Cortana and Live Tiles|TLSv1.2/HTTPS/HTTP|www.bing.com*|
|||HTTPS/HTTP|fp.msedge.net|
|||TLSv1.2|odinvzc.azureedge.net|
|||TLSv1.2|b-ring.msedge.net|
|Device metadata|The following endpoint is used to retrieve device metadata.|TLSv1.2/HTTP|dmd.metaservices.microsoft.com|
|Diagnostic data|The following endpoints are used by the Connected User Experiences and Telemetry component and connects to the Microsoft Data Management service. <br/>If you turn off traffic for this endpoint, diagnostic and usage information, which helps Microsoft find and fix problems and improve our products and services, won't be sent back to Microsoft.|TLSv1.2/HTTP|v10.events.data.microsoft.com|
||The following endpoints are used by Windows Error Reporting.|TLSv1.2/HTTPS/HTTP|watson.telemetry.microsoft.com|
|Font Streaming|The following endpoints are used to download fonts on demand.|TLSv1.2/HTTPS|fs.microsoft.com*|
|Licensing|The following endpoint is used for online activation and some app licensing.|HTTPS/HTTP|*licensing.mp.microsoft.com|
|Location|The following endpoints are used for location data.|TLSV1.2|inference.location.live.net|
|Maps|The following endpoints are used to check for updates to maps that have been downloaded for offline use.|HTTPS/HTTP|maps.windows.com|
|Microsoft Account|The following endpoints are used for Microsoft accounts to sign in|TLSv1.2/HTTPS/HTTP|*login.live.com|
|Microsoft Edge|The following endpoint is used by Microsoft Edge Update service to check for new updates. If you disable this endpoint, Microsoft Edge won’t be able to check for and apply new edge updates.|HTTPS/HTTP|msedge.api.cdp.microsoft.com|
|Microsoft Store|The following endpoint is used to download image files that are called when applications run (Microsoft Store or Inbox MSN Apps)|TLSv1.2/HTTPS/HTTP|img-prod-cms-rt-microsoft-com.akamaized.net|
||The following endpoint is used for the Windows Push Notification Services (WNS). WNS enables third-party developers to send toast, tile, badge, and raw updates from their own cloud service. This provides a mechanism to deliver new updates to your users in a power-efficient and dependable way.|TLSv1.2/HTTPS|*.wns.windows.com|
||The following endpoint is used to revoke licenses for malicious apps in the Microsoft Store.|TLSv1.2/HTTPS/HTTP|storecatalogrevocation.storequality.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|1storecatalogrevocation.storequality.microsoft.com|
||The following endpoints are used to communicate with Microsoft Store.|TLSv1.2/HTTPS/HTTP|*displaycatalog.mp.microsoft.com|
|||HTTPS|storesdk.dsx.mp.microsoft.com|
||The following endpoint is used to get Microsoft Store analytics.|TLSv1.2/HTTPS/HTTP|manage.devcenter.microsoft.com|
|Network Connection Status Indicator (NCSI)|Network Connection Status Indicator (NCSI) detects Internet connectivity and corporate network connectivity status. NCSI sends a DNS request and HTTP query to this endpoint to determine if the device can communicate with the Internet.|TLSv1.2/HTTP|www.msftconnecttest.com*|
|Office|The following endpoints are used to connect to the Office 365 portal's shared infrastructure, including Office in a browser.|TLSv1.2/HTTPS|office.com|
|||HTTPS/HTTP|officehomeblobs.blob.core.windows.net|
|||TLSv1.2|self.events.data.microsoft.com|
|OneDrive|The following endpoints are related to OneDrive.|HTTPS|g.live.com|
|||TLSv1.2/HTTPS|oneclient.sfx.ms|
|||HTTPS/TLSv1.2|logincdn.msauth.net|
|Settings|The following endpoint is used as a way for apps to dynamically update their configuration. Apps such as System Initiated User Feedback and the Xbox app use it.|TLSv1.2/HTTPS/HTTP|settings.data.microsoft.com*|
|||TLSv1.2/HTTPS/HTTP|settings-win.data.microsoft.com*|
|Skype|The following endpoint is used to retrieve Skype configuration values.|TLSv1.2/HTTPS/HTTP|*.pipe.aria.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|config.edge.skype.com|
|Teams|The following endpoint is used for Microsoft Teams application.|TLSv1.2/HTTPS/HTTP|config.teams.microsoft.com|
|Microsoft Defender Antivirus|The following endpoints are used for Windows Defender when Cloud-based Protection is enabled|TLSv1.2/HTTPS|wdcp.microsoft.com</br>wdcpalt.microsoft.com|
|||HTTPS/HTTP|*.smartscreen-prod.microsoft.com|
||The following endpoints are used for Windows Defender SmartScreen reporting and notifications.|TLSv1.2|*.smartscreen.microsoft.com|
|||TLSv1.2/HTTP|checkappexec.microsoft.com|
|Windows Spotlight|The following endpoints are used to retrieve Windows Spotlight metadata that describes content, such as references to image locations, as well as suggested apps, Microsoft account notifications, and Windows tips.|TLSv1.2/HTTPS/HTTP|arc.msn.com*</br>ris.api.iris.microsoft.com|
|Windows Update|The following endpoint is used for Windows Update downloads of apps and OS updates, including HTTP downloads or HTTP downloads blended with peers.|TLSv1.2/HTTPS/HTTP|*.prod.do.dsp.mp.microsoft.com|
|||TLSv1.2/HTTPS/HTTP|*.dl.delivery.mp.microsoft.com|
||The following endpoints are used to download operating system patches, updates, and apps from Microsoft Store.|TLSv1.2/HTTP|*.windowsupdate.com|
|||TLSv1.2/HTTPS/HTTP|*.delivery.mp.microsoft.com|
||The following endpoints enable connections to Windows Update, Microsoft Update, and the online services of the Store to help keep the device secure.|TLSv1.2/HTTPS/HTTP|*.update.microsoft.com|
||The following endpoint is used for compatibility database updates for Windows.|HTTPS/HTTP|adl.windows.com|
||The following endpoint is used for content regulation.|TLSv1.2/HTTPS/HTTP|tsfe.trafficshaping.dsp.mp.microsoft.com|
|Xbox Live|The following endpoints are used for Xbox Live.|TLSv1.2/HTTPS/HTTP|dlassets-ssl.xboxlive.com|
|||TLSv1.2/HTTPS|da.xboxservices.com|
