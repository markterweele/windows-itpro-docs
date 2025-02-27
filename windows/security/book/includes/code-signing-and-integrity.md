---
author: paolomatarazzo
ms.author: paoloma
ms.date: 12/11/2024
ms.topic: include
---

## Code signing and integrity

To ensure that Windows files haven't been tampered with, the Windows Code Integrity process verifies the signature of each file in Windows. Code signing is core to establishing the integrity of firmware, drivers, and software across the Windows platform. Code signing creates a digital signature by encrypting the hash of the file with the private key portion of a code-signing certificate and embedding the signature into the file. The Windows code integrity process verifies the signed file by decrypting the signature to check the integrity of the file and confirm that it is from a reputable publisher, ensuring that the file hasn't been tampered with.

The digital signature is evaluated across the Windows environment on Windows boot code, Windows kernel code, and Windows user mode applications. Secure Boot and Code Integrity verify the signature on bootloaders, Option ROMs, and other boot components to ensure that it's trusted and from a reputable publisher. For drivers not published by Microsoft, Kernel Code Integrity verifies the signature on kernel drivers and requires that drivers be signed by Windows or certified by the [Windows Hardware Compatibility Program (WHCP)](/windows-hardware/design/compatibility/). This program ensures that third-party drivers are compatible with various hardware and Windows and that the drivers are from vetted driver developers.
