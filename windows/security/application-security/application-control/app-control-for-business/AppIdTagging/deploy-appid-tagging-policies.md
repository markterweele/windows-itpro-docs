---
title: Deploying App Control for Business AppId tagging policies
description: How to deploy your App Control AppId tagging policies locally and globally within your managed environment.
ms.localizationpriority: medium
ms.date: 09/11/2024
ms.topic: install-set-up-deploy
---

# Deploying App Control for Business AppId tagging policies

[!INCLUDE [Feature availability note](../includes/feature-availability-note.md)]

Similar to App Control for Business policies, App Control AppId tagging policies can be deployed locally and to your managed endpoints several ways. Once you've created your AppId tagging policy, use one of the following methods to deploy:

1. [Deploy AppId tagging policies with MDM](#deploy-appid-tagging-policies-with-mdm)
1. [Deploy policies with Configuration Manager](#deploy-appid-tagging-policies-with-configuration-manager)
1. [Deploy policies using scripting](#deploy-appid-tagging-policies-via-scripting)
1. [Deploy using the ApplicationControl CSP](#deploying-policies-via-the-applicationcontrol-csp)

## Deploy AppId tagging policies with MDM

Custom AppId tagging policies can be deployed to endpoints using [the OMA-URI feature in MDM](../deployment/deploy-appcontrol-policies-using-intune.md#deploy-app-control-policies-with-custom-oma-uri).

## Deploy AppId tagging policies with Configuration Manager

Custom AppId tagging policies can be deployed via Configuration Manager using the [deployment task sequences](../deployment/deploy-appcontrol-policies-with-memcm.md#deploy-custom-app-control-policies-using-packagesprograms-or-task-sequences), policies can be deployed to your managed endpoints and users.

### Deploy AppId tagging Policies via Scripting

Scripting hosts can be used to deploy AppId tagging policies as well. This approach is often best suited for local deployment, but works for deployment to managed endpoints and users too. For more information on how to deploy App Control AppId tagging policies via scripting, see [Deploy App Control policies using script](../deployment/deploy-appcontrol-policies-with-script.md). For AppId tagging policies, the only applicable method is deploying to version 1903 or later.

### Deploying policies via the ApplicationControl CSP

Multiple App Control policies can be managed from an MDM server through ApplicationControl configuration service provider (CSP). The CSP also provides support for rebootless policy deployment.

However, when policies are unenrolled from an MDM server, the CSP will attempt to remove every policy from devices, not just the policies added by the CSP. The reason for this is that the ApplicationControl CSP doesn't track enrollment sources for individual policies, even though it will query all policies on a device, regardless if they were deployed by the CSP.

For more information, see [ApplicationControl CSP](/windows/client-management/mdm/applicationcontrol-csp) to deploy multiple policies, and optionally use Microsoft Intune's Custom OMA-URI capability.

> [!NOTE]
> WMI and GP don't currently support multiple policies. If you can't directly access the MDM stack, use the [ApplicationControl CSP via the MDM Bridge WMI Provider](/windows/client-management/mdm/applicationcontrol-csp#powershell-and-wmi-bridge-usage-guidance) to manage multiple policy format App Control for Business policies.
