---
title: WESL_UserSetting.SetCustomShell
description: WESL_UserSetting.SetCustomShell
ms.date: 3/7/2025
ms.topic: reference
---

# WESL_UserSetting.SetCustomShell

This method configures Shell Launcher for a specific user or group, based on the security identifier (SID).

[!INCLUDE [shell-launcher](../../../includes/licensing/shell-launcher.md)]

## Syntax

```mof
[Static] uint32 SetCustomShell (
    [In, Required] string Sid,
    [In, Required] string Shell,
    [In] sint32 CustomReturnCodes[],
    [In] sint32 CustomReturnCodesAction[],
    [In] sint32 DefaultAction
);
```

## Parameters

**Sid**<br/>\[in, required\] A string containing the security identifier (SID) of the user or group that Shell Launcher is being configured for.

**Shell**<br/>\[in, required\] The application or executable that Shell Launcher starts as the shell.

**CustomReturnCodes**<br/>\[in\] An array of custom return codes that can be returned by the shell application.

**CustomReturnCodesAction**<br/>\[in\] An array of custom return code actions that determine the action that Shell Launcher takes when the shell application exits. The custom actions map to the array of *CustomReturnCodes*.

The possible actions are defined in the following table:

| Value | Description |
|:-----:|-------------|
| 0 | Restart the shell. |
| 1 | Restart the device. |
| 2 | Shut down the device. |
| 3 | Do nothing. |

**DefaultAction**<br/>\[In\] The default action that Shell Launcher takes when the shell application exits.

The possible actions are defined in the following table:

| Value | Description |
|:-----:|-------------|
| 0 | Restart the shell.|
| 1 | Restart the device. |
| 2 | Shut down the device. |
| 3 | Do nothing. |

## Return Value

Returns an HRESULT value that indicates [WMI status](/windows/win32/wmisdk/wmi-non-error-constants) or a [WMI error](/windows/win32/wmisdk/wmi-error-constants).

## Remarks

Shell Launcher uses the *CustomReturnCodes* and *CustomReturnCodesAction* arrays to determine the system behavior when the shell application exits, based on the return value of the shell application.

If the return value does not exist in *CustomReturnCodes*, or if the corresponding action defined in *CustomReturnCodesAction* is not a valid value, Shell Launcher uses *DefaultAction* to determine system behavior. If *DefaultAction* is not defined, or is not a valid value, Shell Launcher restarts the shell application.
