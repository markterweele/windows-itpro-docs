---
title: Microsoft Connected Cache Release Notes
description: Release Notes for Microsoft Connected Cache for Enterprise and Education.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: release-notes
ms.author: lichris
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
ms.date: 10/30/2024
---

# Release Notes for Microsoft Connected Cache for Enterprise and Education

This article contains details about the latest releases of Connected Cache. Since Connected Cache is a preview service, some releases may contain breaking changes.

## February 2025 Release

Released on **2/27/2025**

This release contains improvements that can only be applied by redeploying your cache nodes using the updated installation script.

### New Connected Cache container version

- v1.2.1.2083_E

### New Linux-hosted installation script version

- v1.08

### New Windows-hosted installation script version

- v2.0.0.3

### Improvements to Windows-hosted cache nodes

- **Connected Cache WSL distribution now uses Ubuntu 24.04**: The Windows Subsystem for Linux (WSL) distribution used by Connected Cache has been updated to Ubuntu 24.04 (was 22.04). This change ensures that the WSL distribution is up-to-date with the latest security patches and features.
- **Connected Cache container now uses Ubuntu 24.04 Docker environment**: The Connected Cache container now runs using an Ubuntu 24.04 Docker environment (was 22.04). This change ensures that the container environment is up-to-date with the latest security patches and features.
- **TLS-inspecting proxies no longer cause IoT Edge error during Connected Cache installation**: Fixed a bug that was causing proxy certificate path string to be improperly handled, leading to IoT Edge errors during Connected Cache installation.
- **Security improvements**: Kept intentionally vague to protect previous versions of Connected Cache.

### Improvements to Linux-hosted cache nodes

- **Connected Cache container now uses Ubuntu 24.04 Docker environment**: The Connected Cache container now runs using an Ubuntu 24.04 Docker environment (was 22.04). This change ensures that the container environment is up-to-date with the latest security patches and features.
- **TLS-inspecting proxies no longer cause IoT Edge error during Connected Cache installation**: Fixed a bug that was causing proxy certificate path string to be improperly handled, leading to IoT Edge errors during Connected Cache installation.
- **Security improvements**: Kept intentionally vague to protect previous versions of Connected Cache.

## Windows-hosted install script v2.0.0.2

Released on **2/7/2025**

This release only contains changes to the Windows-hosted installation scripts for Connected Cache. To take advantage of these changes, you need to redeploy your existing cache nodes using the updated installation script.

### Improvements

- **Removes dependency on AMQP/MQTT ports**: Cache nodes deployed using this updated installation script will no longer use AMQP (5671) or MQTT (8883) ports. This change simplifies the network configuration for cache nodes and reduces the number of ports that need to be opened in your network security group.
- **Improves cleanup during uninstall**: Windows-hosted cache nodes will now remove port proxy rules when uninstalled using the `uninstallmcconwsl.ps1` script. This change ensures that the host machine's WSL port-forwarding rules are cleaned up properly when uninstalling Connected Cache.
- **Changes install error codes from decimal to hex code**: Install error codes for Windows-hosted cache nodes are now displayed in hex code format, improving error code readability.
- **Uses configured proxy to perform install**: If a proxy was configured for the Windows-hosted cache node in Azure portal, the cache node uses the specified proxy during installation.

## Public Preview Release

Released on **10/30/2024**

For customers that installed earlier versions of Connected Cache, this release contains breaking changes that affect both Linux-hosted and Windows-hosted cache nodes. See the [early preview documentation page](mcc-ent-early-preview.md) for more details.

### New Connected Cache container version

- v1.2.1.2076_E

### Feature updates

- **Metrics and charts in Azure portal**: You can now visualize *Outbound egress* and *Volume by Content type* charts for your cache node on Azure portal. You can also create custom monitoring charts for your cache nodes. This capability is under the **Metrics** tab on Azure portal.
- **Cache nodes for Windows or Linux host machines**: Cache nodes can now be created and deployed to Windows host machine or Linux host machines by choosing the OS when creating cache nodes.
- **Ubuntu 22.04 LTS**: Cache nodes can now be deployed on Ubuntu 22.04 LTS.
- **Azure CLI support**: Cache nodes can now be created and managed via Azure CLI.
- **Proxy**: We added support for unauthenticated proxy and cloud proxy integration.
- **Updates**: Your cache nodes are now updated automatically and we also added the capability to set each cache node's update ring to govern the cadence of Microsoft Connected Cache container updates.

### Fixes
- We fixed various bugs to achieve a smoother installation experience.

## Related content

- [Overview of Connected Cache](mcc-ent-edu-overview.md)
