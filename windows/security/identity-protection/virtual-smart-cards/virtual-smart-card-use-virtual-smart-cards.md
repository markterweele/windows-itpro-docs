---
title: Use Virtual Smart Cards
description: Learn about the requirements for virtual smart cards, how to use and manage them.
ms.topic: concept-article
ms.date: 04/07/2025
---

# Use Virtual Smart Cards

[!INCLUDE [virtual-smart-card-deprecation-notice](../../includes/virtual-smart-card-deprecation-notice.md)]

Learn about the requirements for virtual smart cards, how to use and manage them.

## Requirements, restrictions, and limitations

| Area | Requirements and details |
|--|--|
| Supported Trusted Platform Module (TPM) | Any TPM that adheres to the TPM main specifications for version 1.2 or version 2.0 (as set by the Trusted Computing Group) is supported for use as a virtual smart card. For more information, see the [TPM Main Specification](http://www.trustedcomputinggroup.org/resources/tpm_main_specification). |
| Supported virtual smart cards per computer | Ten smart cards can be connected to a computer or device at one time. This includes physical and virtual smart cards combined. <br><br>**Note**<br>You can create more than one virtual smart card; however, after creating more than four virtual smart cards, you may start to notice performance degradation. Because all smart cards appear as if they're always inserted, if more than one person shares a computer or device, each person can see all the virtual smart cards that are created on that computer or device. If the user knows the PIN values for all the virtual smart cards, the user will also be able to use them.<br> |
| Supported number of certificates on a virtual smart card | A single TPM virtual smart card can contain 30 distinct certificates with the corresponding private keys. Users can continue to renew certificates on the card until the total number of certificates on a card exceeds 90. The reason that the total number of certificates is different from the total number of private keys is that sometimes the renewal can be done with the same private key—in which case a new private key isn't generated. |
| PIN, PIN Unlock Key (PUK), and Administrative key requirements | The PIN and the PUK must be a minimum of eight characters that can include numerals, alphabetic characters, and special characters.<br>The Administrative key must be entered as 48 hexadecimal characters. It's a 3-key triple DES with ISO/IEC 9797 padding method 2 in CBC chaining mode. |

## Using Tpmvscmgr.exe

To create and delete TPM virtual smart cards for end users, the Tpmvscmgr command-line tool is included as a command-line tool with the operating system. You can use the **Create** and **Delete** parameters to manage virtual smart cards on local or remote computers. For information about using this tool, see [Tpmvscmgr](virtual-smart-card-tpmvscmgr.md).

## Create and delete virtual smart cards programmatically

Virtual smart cards can also be created and deleted by using APIs. For more information, see the following classes and interfaces:

- [TpmVirtualSmartCardManager](/previous-versions/windows/desktop/legacy/hh707171(v=vs.85))
- [RemoteTpmVirtualSmartCardManager](/previous-versions/windows/desktop/legacy/hh707166(v=vs.85))
- [ITpmVirtualSmartCardManager](/windows/win32/api/tpmvscmgr/nn-tpmvscmgr-itpmvirtualsmartcardmanager)
- [ITPMVirtualSmartCardManagerStatusCallBack](/windows/win32/api/tpmvscmgr/nn-tpmvscmgr-itpmvirtualsmartcardmanagerstatuscallback)

You can use APIs in the `Windows.Device.SmartCards` namespace to build Microsoft Store apps to manage the full lifecycle of virtual smart cards. For information about how to build an app to do this, see [Strong Authentication: Building Apps That Leverage Virtual Smart Cards in Enterprise, BYOD, and Consumer Environments](https://channel9.msdn.com/events/build/2013/2-041).

The following table describes the features that can be developed in a Microsoft Store app:

| Feature | Physical Smart Card | Virtual Smart Card |
|--|--|--|
| Query and monitor smart card readers | Yes | Yes |
| List available smart cards in a reader, and retrieve the card name and card ID | Yes | Yes |
| Verify if the administrative key of a card is correct | Yes | Yes |
| Provision (or reformat) a card with a given card ID | Yes | Yes |
| Change the PIN by entering the old PIN and specifying a new PIN | Yes | Yes |
| Change the administrative key, reset the PIN, or unblock the smart card by using a challenge/response method | Yes | Yes |
| Create a virtual smart card | Not applicable | Yes |
| Delete a virtual smart card | Not applicable | Yes |
| Set PIN policies | No | Yes |

For more information about these Windows APIs, see:

- [Windows.Devices.SmartCards namespace (Windows)](/uwp/api/Windows.Devices.SmartCards)
- [Windows.Security.Cryptography.Certificates namespace (Windows)](/uwp/api/Windows.Security.Cryptography.Certificates)

## Distinguishing TPM-based virtual smart cards from physical smart cards

To help users visually distinguish a Trusted Platform Module (TPM)-based virtual smart card from physical smart cards, the virtual smart card has a different icon. The virtual smart card icon :::image type="icon" source="images/virtual-smart-card-icon.svg" border="false"::: is displayed during sign-in, and on other screens that require the user to enter the PIN for a virtual smart card.

A TPM-based virtual smart card is labeled *Security Device* in the user interface.

## Changing the PIN

The PIN for a virtual smart card can be changed by following these steps:

- Sign in with the old PIN or password
- Press <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> and select **Change a password**
- Select **Sign-in Options**
- Select the virtual smart card icon
- Enter and confirm the new PIN

## Resolving issues

### TPM not provisioned

For a TPM-based virtual smart card to function properly, a provisioned TPM must be available on the computer:

- If the TPM is disabled in the BIOS, or it isn't provisioned with full ownership and the storage root key, the TPM virtual smart card creation fails
- If the TPM is initialized after creating a virtual smart card, the card will no longer function, and it must be re-created
- If the operating system is reinstalled, prior TPM virtual smart cards are no longer available and need to be re-created
- If the operating system is upgraded, prior TPM virtual smart cards are available to use in the upgraded operating system

### TPM in lockout state

Sometimes, due to frequent incorrect PIN attempts from a user, the TPM may enter the lockout state. To resume using the TPM virtual smart card, it's necessary to reset the lockout on the TPM by using the owner's password or to wait for the lockout to expire. Unblocking the user PIN doesn't reset the lockout in the TPM. When the TPM is in lockout, the TPM virtual smart card appears as if it's blocked. When the TPM enters the lockout state because the user entered an incorrect PIN too many times, it may be necessary to reset the user PIN by using the virtual smart card management tools, such as Tpmvscmgr command-line tool.

## See also

For information about authentication, confidentiality, and data integrity use cases, see [Virtual Smart Card Overview](virtual-smart-card-overview.md).
