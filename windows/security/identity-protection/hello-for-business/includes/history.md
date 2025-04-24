---
author: paolomatarazzo
ms.author: paoloma
ms.date: 03/12/2024
ms.topic: include
---

### History

This setting specifies the number of past PINs that can be associated to a user account that can't be reused. This policy enhances security by ensuring that old PINs are not reused continually. The value must be between 0 to 50 PINs. If this policy is set to 0, then storage of previous PINs is not required.

The default value is 0.

> [!NOTE]
> PIN history is not preserved through PIN reset.

|  | Path |
|--|--|
| **CSP** | `./Device/Vendor/MSFT/PassportForWork/{TenantId}/Policies/PINComplexity/`[devicetenantidpoliciespincomplexityhistory](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexityhistory)<br><br>`./User/Vendor/MSFT/PassportForWork/{TenantId}/Policies/PINComplexity/`[usertenantidpoliciespincomplexityhistory](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityhistory) |
| **GPO** | **Computer Configuration** > **Administrative Templates** > **System** > **PIN Complexity** |

> [!NOTE]
> Starting with Windows 11, version 23H2, Windows Hello uses Virtualization-based security (VBS) to isolate credentials on devices that support [Enhanced Security Settings (ESS)](/windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security).
>
> Starting with Windows 11, version 24H2, Windows Hello uses VBS to isolate credentials on all devices that have VBS enabled.
>
> On such devices, PIN history is not supported.
