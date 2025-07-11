---
title: Understanding App Control event tags
description: Learn what different App Control for Business event tags signify.
ms.localizationpriority: medium
ms.date: 09/11/2024
ms.topic: article
---

# Understanding App Control event tags

App Control for Business events include many fields, which provide helpful troubleshooting information to figure out exactly what an event means. This article describes the values and meanings for a few useful event tags.

## SignatureType

Represents the type of signature which verified the image.

| SignatureType Value | Explanation |
|---|----------|
| 0 | Unsigned or verification hasn't been attempted |
| 1 | Embedded signature |
| 2 | Cached signature; presence of a CI EA means the file was previously verified |
| 3 | Cached catalog verified via Catalog Database or searching catalog directly |
| 4 | Uncached catalog verified via Catalog Database or searching catalog directly |
| 5 | Successfully verified using an EA that informs CI that catalog to try first |
| 6 | AppX / MSIX package catalog verified |
| 7 | File was verified |

## Requested and Validated Signing Level

Represents the signature level at which the code was verified.

| SigningLevel Value | Explanation |
|---|----------|
| 0 | Signing level hasn't yet been checked |
| 1 | File is unsigned or has no signature that passes the active policies |
| 2 | Trusted by App Control for Business policy |
| 3 | Developer signed code |
| 4 | Authenticode signed |
| 5 | Microsoft Store signed app PPL (Protected Process Light) |
| 6 | Microsoft Store-signed |
| 7 | Signed by an Antimalware vendor whose product is using AMPPL |
| 8 | Microsoft signed |
| 11 | Only used for signing of the .NET NGEN compiler |
| 12 | Windows signed |
| 14 | Windows Trusted Computing Base signed |

## VerificationError

Represents why verification failed, or if it succeeded.

| VerificationError Value | Explanation |
|---|----------|
| 0 | Successfully verified signature. |
| 1 | File has an invalid hash. |
| 2 | File contains shared writable sections. |
| 3 | File isn't signed. |
| 4 | Revoked signature. |
| 5 | Expired signature. |
| 6 | File is signed using a weak hashing algorithm, which doesn't meet the minimum policy. |
| 7 | Invalid root certificate. |
| 8 | Signature was unable to be validated; generic error. |
| 9 | Signing time not trusted. |
| 10 | The file must be signed using page hashes for this scenario. |
| 11 | Page hash mismatch. |
| 12 | Not valid for a PPL (Protected Process Light). |
| 13 | Not valid for a PP (Protected Process). |
| 14 | The signature is missing the required ARM processor EKU. |
| 15 | Failed WHQL check. |
| 16 | Default policy signing level not met. |
| 17 | Custom policy signing level not met; returned when signature doesn't validate against an SBCP-defined set of certs. |
| 18 | Custom signing level not met; returned if signature fails to match `CISigners` in UMCI. |
| 19 | Binary is revoked based on its file hash. |
| 20 | SHA1 cert hash's timestamp is missing or after valid cutoff as defined by Weak Crypto Policy. |
| 21 | Failed to pass App Control for Business policy. |
| 22 | Not Isolated User Mode (IUM) signed; indicates an attempt to load a standard Windows binary into a virtualization-based security (VBS) trustlet. |
| 23 | Invalid image hash. This error can indicate file corruption or a problem with the file's signature. Signatures using elliptic curve cryptography (ECC), such as ECDSA, return this VerificationError. |
| 24 | Flight root not allowed; indicates trying to run flight-signed code on production OS. |
| 25 | Anti-cheat policy violation. |
| 26 | Explicitly denied by App Control policy. |
| 27 | The signing chain appears to be tampered/invalid. |
| 28 | Resource page hash mismatch. |

## Policy activation event Options

The App Control policy rule option values can be derived from the "Options" field in the Details section for successful [policy activation events](event-id-explanations.md#app-control-policy-activation-events). To parse the values, first convert the hex value to binary. To derive and parse these values, follow the below workflow.

- Access Event Viewer.
- Access the Code integrity 3099 event.
- Access the details pane.
- Identify the hex code listed in the "Options" field.
- Convert the hex code to binary.

:::image type="content" source="../images/event-3099-options.png" alt-text="Event 3099 policy rule options.":::

For a simple solution for converting hex to binary, follow these steps:

1. Open the Calculator app.
1. Select the menu icon. :::image type="icon" source="../images/calculator-menu-icon.png" border="false":::
1. Select **Programmer** mode.
1. Select **HEX**. :::image type="icon" source="../images/hex-icon.png" border="false":::
1. Enter your hex code. For example, `80881000`.
1. Switch to the **Bit Toggling Keyboard**. :::image type="icon" source="../images/bit-toggling-keyboard-icon.png" border="false":::

:::image type="content" source="../images/calculator-with-hex-in-binary.png" alt-text="An example of the calculator app in programmer mode, with a hex code converted into binary.":::

This view provides the hex code in binary form, with each bit address shown separately.  The bit addresses start at 0 in the bottom right.  Each bit address correlates to a specific event policy-rule option.  If the bit address holds a value of 1, the setting is in the policy.

Next, use the bit addresses and their values from the following table to determine the state of each [policy rule-option](../design/select-types-of-rules-to-create.md#table-1-app-control-for-business-policy---policy-rule-options). For example, if the bit address of 16 holds a value of 1, then the **Enabled: Audit Mode (Default)** option is in the policy. This setting means that the policy is in audit mode.

| Bit Address | Policy Rule Option |
|-------|------|
| 2 | `Enabled:UMCI` |
| 3 | `Enabled:Boot Menu Protection` |
| 4 | `Enabled:Intelligent Security Graph Authorization` |
| 5 | `Enabled:Invalidate EAs on Reboot` |
| 7 | `Required:WHQL` |
| 10 | `Enabled:Allow Supplemental Policies` |
| 11 | `Disabled:Runtime FilePath Rule Protection` |
| 13 | `Enabled:Revoked Expired As Unsigned` |
| 16 | `Enabled:Audit Mode (Default)` |
| 17 | `Disabled:Flight Signing` |
| 18 | `Enabled:Inherit Default Policy` |
| 19 | `Enabled:Unsigned System Integrity Policy (Default)` |
| 20 | `Enabled:Dynamic Code Security` |
| 21 | `Required:EV Signers` |
| 22 | `Enabled:Boot Audit on Failure` |
| 23 | `Enabled:Advanced Boot Options Menu` |
| 24 | `Disabled:Script Enforcement` |
| 25 | `Required:Enforce Store Applications` |
| 27 | `Enabled:Managed Installer` |
| 28 | `Enabled:Update Policy No Reboot` |

## Microsoft Root CAs trusted by Windows

The Microsoft Root certificates can be allowed and denied in policy using 'WellKnown' rules. The mapping between the root's ASN1 encoded RSA PKCS#1 public key and the WellKnown values, expressed in hexidecimal, are listed below

| Root ID | Root Name | Root Public Key |
|---|----------|
| 0| None | N/A |
| 1| Unknown | N/A |
| 2 | Self-Signed | N/A |
| 3 | Microsoft Authenticode(tm) Root Authority  | `3082010A0282010100DF08BAE33F6E649BF589AF28964A078F1B2E8B3E1DFCB88069A3A1CEDBDFB08E6C8976294FCA603539AD7232E00BAE293D4C16D94B3C9DDAC5D3D109C92C6FA6C2605345DD4BD155CD031CD2595624F3E578D807CCD8B31F903FC01A71501D2DA712086D7CB0866CC7BA853207E1616FAF03C56DE5D6A18F36F6C10BD13E69974872C97FA4C8C24A4C7EA1D194A6D7DCEB05462EB818B4571D8649DB694A2C21F55E0F542D5A43A97A7E6A8E504D2557A1BF1B1505437B2C058DBD3D038C93227D63EA0A5705060ADB6198652D4749A8E7E656755CB8640863A9304066B2F9B6E334E86730E1430B87FFC9BE72105E23F09BA74865BF09887BCD72BC2E799B7B0203010001` |
| 4 | Microsoft Product Root 1997 | `3082010A0282010100A902BDC170E63BF24E1B289F97785E30EAA2A98D255FF8FE954CA3B7FE9DA2203E7C51A29BA28F60326BD1426479EEAC76C954DAF2EB9C861C8F9F8466B3C56B7A6223D61D3CDE0F0192E896C4BF2D669A9A682699D03A2CBF0CB55826C146E70A3E38962CA92839A8EC498342E3840FBB9A6C5561AC827CA1602D774CE999B4643B9A501C310824149FA9E7912B18E63D986314605805659F1D375287F7A7EF9402C61BD3BF5545B38980BF3AEC54944EAEFDA77A6D744EAF18CC96092821005790606937BB4B12073C56FF5BFBA4660A08A6D2815657EFB63B5E16817704DAF6BEAE8095FEB0CD7FD6A71A725C3CCABCF008A32230B30685C9B320771385DF0203010001` |
| 5 | Microsoft Product Root 2001 | `3082020A0282020100F35DFA8067D45AA7A90C2C9020D035083C7584CDB707899C89DADECEC360FA91685A9E94712918767CC2E0C82576940E58FA043436E6DFAFF780BAE9580B2B93E59D05E3772291F734643C22911D5EE10990BC14FEFC755819E179B70792A3AE885908D89F07CA0358FC68296D32D7D2A8CB4BFCE10B48324FE6EBB8AD4FE45C6F139499DB95D575DBA81AB79491B4775BF5480C8F6A797D1470047D6DAF90F5DA70D847B7BF9B2F6CE705B7E11160AC7991147CC5D6A6E4E17ED5C37EE592D23C00B53682DE79E16DF3B56EF89F33C9CB527D739836DB8BA16BA295979BA3DEC24D26FF0696672506C8E7ACE4EE1233953199C835084E34CA7953D5B5BE6332594036C0A54E044D3DDB5B0733E458BFEF3F5364D842593557FD0F457C24044D9ED6387411972290CE684474926FD54B6FB086E3C73642A0D0FCC1C05AF9A361B9304771960A16B091C04295EF107F286AE32A1FB1E4CD033F777104C720FC490F1D4588A4D7CB7E88AD8E2DEC45DBC45104C92AFCEC869E9A11975BDECE5388E6E2B7FDAC95C22840DBEF0490DF813339D9B245A5238706A5558931BB062D600E41187D1F2EB597CB11EB15D524A594EF151489FD4B73FA325BFCD13300F95962700732EA2EAB402D7BCADD21671B30998F16AA23A841D1B06E119B36C4DE40749CE15865C1601E7A5B38C88FBB04267CD41640E5B66B6CAA86FD00BFCEC1350203010001`|
| 6 | Microsoft Product Root 2010 | `3082020A028202010095E3A8C1B99C2654B099EF261FAC1EC73080BBF53FF2E4BBF8FE066A0AA688BCB48C45E070551988B405CBB5C1A1FAD47CC24253079C5456A897E09469BE1324EFE58A299CA6D02B2F8AA6E879442E8BEAC9BEB8548653BE07243454152220017B8A46FBD291079509B05611CC76B2D01F4479523428EC4F49C2CB61D386DCE4A37E559E9FEE106FCFE13DF8B78479A23B8D1CB0817CE44407E4CE46B098838D878FE5F5AE407AF1ED3D9B9A7C4AD1B9C394057BDCDAB8CEDC1E6CCFD99E37EFC35A367B908645DCF62ECADDEEDE27D9749A69F5D95D092D4541CCB7C282D42A8C162592973D944E89337E5B0354CDB083A08E41B7878DD9056352F6EEE64E139D54CD49FEE38B3B509B48BBB2E592D4ABA0C510AF3EB145213490DCADB9F7FE21AEEE50587A3AE5AAD8E382D6CF6D4DC915AC9C3117A516A742F6DA1278A76690ECFCCD0163FFF00EBAE1CDF0DB6B9A0FF60F040109BC9FCEB76C517057081BFF799A525DBAAC14E53B67CF2C52DE279A34036E2548B01974FC4D98C24B8C92E188AE482AABABCD144DB6610EA1098F2CDB45AF7D3B815608C93B41B7649F5D2E127FB969291F52454A23C6AFB6B238729D0833FFD0CF89B6EA6E8544943E9159EBEF9EBD9B9C1A47034EA21796FA620BE853B64EE3E82A7359E213B8F85A7EC6E20ADD4A43CCC3773B7A31040AC184963A636E1A3E0A0C25B87EB5520CB9AB0203010001`|
| 7 | Microsoft Standard Root 2011 | `3082020A0282020100B28041AA35384D13723268224DB8B2F1FFD552BC6CC7F5D24A8C36EED1C25C7E8C8AAEAF13286FC073E33ACED025A85A3A6DEFA8B859AB132368CD0C2987D16F805C8F447F5D90015258AC51C55F2A87DCDCD80A1DC103B97BB056E8A3DE6461C29EF8F37CB9EC0DB554FE4CB6654F88F09C48990C420B097C315917790678288D893A4C0325BE716A5C0BE78460A49922E3D2AF84A4A7FBD198ED0CA9DE9489E10EA0DCC0CE993DEA0852BB5679E41F84BA1EB8B4C4495C4F314B87DDDD0567269980E07111A3B8A541E2A453B9F73229830C13BF365E04B34B43472F6BE2911ED3984FDD4207C8E81D12FC99A96B3E927EC8D6693AFC64BDB6099DCAFD0C0BA29B77604B0394A4306912D6422DC1414CCADCAAFD8F5B83469AD9FCB1D1E3B3C97F487ACD24F0418F5C74D0ACB010200649B7C72D21C857E3D086F30368FBD0CE71C189994A64016CFDEC3091CF413C92C7E5BA861D6184C75F833962AEB4922F47F30BF855EBA01F59D0BB749B1ED076E6F2E906D710E8FA64DE69C635968802F046B83F27996FCB71892935F7481602358FD5797C4D02CF5FEB8A834F457188F9A90D4E72E9C29C07CF491B4E040E63518C5ED800C1552CB6C6E0C2654EC93439F59CB3C47EE8616E135F15C45FD97EED1DCEEE44ECCB2E86B1EC38F670EDAB5C13C1D90F0DC780B255ED34F7AC9BE4C3DAE7473CA6B58F31DFC54BAFEBF10203010001`|
| 8 | Microsoft Code Verification Root 2006 | `3082020A0282020100BD77C91C7F157838C50743215AFBE4CC3BC65531FC2189B1BCE7019CFB90BE20115576A74D02E7B2F42E8DEFB2874656CA47CEC8C363E308034B9606B9702244E64B7B443F75B7B8A62B910841EF4B0759D6A4199DF6CBA4BB8E02654DCADE0FB49022F1B56B5C22F6CAF938AA280B062D3C198DB7355F83EDDD65738446929F44E2894A8CD598A76D3DE819CB44AD180BEA5C5F7C0BC39A936844F3B6BF979930723F2859D070C8055778F54A82340A24C17AB064A53A6E12D5036138BB0E2DFD859CD648756A1CB2A2E891FAB7E4F53C5FFDC940ACC7A042F574D8B9DBD7FE73771AE0C4B709B1059A6DE35E8038757852B612D379AE43F765A7D1166469858F783AB894BF4512625A4D8748D6F819BC590106F51ADB60299F013F6E73F9FD8045CE95D78AF6920CC173402C6DAA32A6F17F30F890F1AE4527B9B40E3002BDC60EEC3C8C5BB63485CF140B0C500DA9E259912EA80139F42C15630480B840DF62F7FEB74C13A82CA966133862FC4070627B7577D52B8E1BA599E5B9B7C7ADEA01A0257B5846525654A2C9922B581D4851C01FFE3700D1E2AB10C2A959E942996E8FB51E4766741E98765757045EBD2F8593D50E0B9F2E7B2664A78612095063E7D1C78E7E0E3B07E7BBE4CD1A40D47ABA05594AD6D0EEDC965E224A271C45E3DEDAB2E9D343FDE96FC0C97D1FFD9F909C862008CC74DC40A729B3AB58656BB10203010001`|
| 9 | Microsoft Test Root 1999 | `3081DF300D06092A864886F70D01010105000381CD003081C90281C100A9AA83586DB5D30C4B5B8090E5C30F280C7E3D3C24C52956638CEEC7834AD88C25D30ED312B7E1867274A78BFB0F05E965C19BD856C293F0FBE95A48857D95AADF0186B733334656CB5B7AC4AFA096533AE9FB3B78C1430CC76E1C2FD155F119B23FF8D6A0C724953BC845256F453A464FD2278BC75075C6805E0D9978617739C1B30F9D129CC4BB327BB24B26AA4EC032B02A1321BEED24F47D0DEAAA8A7AD28B4D97B54D64BAFB46DD696F9A0ECC5377AA6EAE20D6219869D946B96432D4170203010001`|
| 0A | Microsoft Test Root 2010 | `3082020A028202010095E3A8C1B99C2654B099EF261FAC1EC73080BBF53FF2E4BBF8FE066A0AA688BCB48C45E070551988B405CBB5C1A1FAD47CC24253079C5456A897E09469BE1324EFE58A299CA6D02B2F8AA6E879442E8BEAC9BEB8548653BE07243454152220017B8A46FBD291079509B05611CC76B2D01F4479523428EC4F49C2CB61D386DCE4A37E559E9FEE106FCFE13DF8B78479A23B8D1CB0817CE44407E4CE46B098838D878FE5F5AE407AF1ED3D9B9A7C4AD1B9C394057BDCDAB8CEDC1E6CCFD99E37EFC35A367B908645DCF62ECADDEEDE27D9749A69F5D95D092D4541CCB7C282D42A8C162592973D944E89337E5B0354CDB083A08E41B7878DD9056352F6EEE64E139D54CD49FEE38B3B509B48BBB2E592D4ABA0C510AF3EB145213490DCADB9F7FE21AEEE50587A3AE5AAD8E382D6CF6D4DC915AC9C3117A516A742F6DA1278A76690ECFCCD0163FFF00EBAE1CDF0DB6B9A0FF60F040109BC9FCEB76C517057081BFF799A525DBAAC14E53B67CF2C52DE279A34036E2548B01974FC4D98C24B8C92E188AE482AABABCD144DB6610EA1098F2CDB45AF7D3B815608C93B41B7649F5D2E127FB969291F52454A23C6AFB6B238729D0833FFD0CF89B6EA6E8544943E9159EBEF9EBD9B9C1A47034EA21796FA620BE853B64EE3E82A7359E213B8F85A7EC6E20ADD4A43CCC3773B7A31040AC184963A636E1A3E0A0C25B87EB5520CB9AB0203010001`|
| 0B | Microsoft DMD Test Root 2005 | `3082010A0282010100BCACAFF12BE9877F310994630F483012C16BEA7E0EFC58B8C890F3C7719F41B5BB29E3834735BF42DE7A9CC16D125094061E721B6FF8C0207FDF6DAD840F08BB9A3F93589D931F05B640AB878C7FAA4F033D7DFA6B3BBCFBE0C426B0173EB67ECC9D089875667A34AF189B3D2CCEFCD943599197F3933255B7DA328ADADE6826C30C6F7EAB434CF5C00A22FD5B47A7A9964617529FBB3B1D850A90CD818105342BCA43C29075574D6151C0D6D2648C412107BE5C824A4F9451087522B9AEB94828F7C78606040B7011F0CDCDA079D3CE9CC5367C579BB6DF5B83BE616BE258D2D9858D7EE1A446574661F9DF4F82B9AC8FD2DFEF6082EC1272BF14D20ACCAF3F0203010001`|
| 0C | Microsoft DMDRoot 2005 | `3082020A0282020100BCFD36D32F1C7CBAC60458F2AB30A3F17DD4B983EF72DB009CCFE65F0CF144BE62225D2F77507CD68539FE7AAE991EC8B3F9C73CC0228DC7A7F9ED87E841ACE42DF2804E148BB4F5250B948D6FB42982CFE69EFDF79FE5B828B7366B2F6D00A449BF78814FA8069433D0D55720A8728BFED7F5632C8D44E960FE2FF539B625069E04C34D952ED52205304A4122610D5A24F0DF636C7FD8D2F69EF35E76E7B4BDBB9589F20AD44E73BD917E46103D2749427489C4E8AAA3A7407785A27F4626CCC6C0CBC3F2B88121A3BB68F3E2E57EF47C7107EBC10AF5DC038C510BE9C71373C1349EABD28E665811A57441CBD2D9E47480F089CB459896D7DB0815A598446CE223785693BC122A854CC29FD15917A1161025FAE7BD141A56F44E396FF563A256C50B7C9FD6F0B068151C6B367171F83983762354F755BC16E30CBC218BDE6DE9EB943D5440C3D320B0AF96BBE7C3B89DFBEEDC9B7153830D9A9FA6B3D216ACEAC8801D8D24243C8291463C497290BA698FBA7A30DDF6A6F13D68E537ED1A43528F19D71A52528CD80FB26428A5ABA70E04A267AA650B666FF696B2905FA5ECAE9BB3B984536DBC5FBE647036E6EE1DD17EB58AE4A137E8DB3E8FC2FDEAE9E35F74B494FCA0206E8FD396146BFBF56AD8122636955F1C7516AD18E50C9AC53774EC0CC367044FD6DAA68096D1263713BD7A0F21892B33B3189B3B37FDE451170203010001`|
| 0D | Microsoft DMD Preview Root 2005 | `3082020A0282020100C3FF519F7576E65C5B6C6EBBB50760626E065740611131724066A5CE94519D702061FCE3C43A49BB6690D5BF94AFEB506B90F3AE5432F01A8AB0EFB064A7CC5EDCEDA6F8DA0FF0430A84B65AC746A1B4D8108CB74924F5FC6F7A4CD1232433E2554EC9778248C08FFDA9F89C189C5A23C608E68CD5C917954E424FA35F3F3649012BA2A1EC4C84FFC182E9B1F2E83773BAA7795AF85A421FDC904665DCE74FC8B3B9501C267F2B7E96790F170EC951E88BEC1E9D425C2DE4907722E6E8411265380A79D128255E67B79B393F76372FB388204E365FF7E952218B5D694CF0146BFFEAD4E8A5E82364E7AACE73E8F5DF25753A0446802321AFC923C322B2631D7B6364FA95FEE16191EBCD2F8755C61DF17B44DABD736FFEE5846569785AE835D35A893968487BB49890DA9FC166E87D5672EA9F73647A2BD0B4F340F0037226F6A0C500B721CC4B9B5E1756A1DA9B45B3B61E300DFFC85F13590147A57AB51950628FFD18ABA29A7CC5EF83CD5A1F00FDC8E854A5B9AEC755B5C572196A370D15A5736C1B9C772DA34B88C338E69044581C54F2EE23048ABAB7D5FEEF22C037163DCFE6D4E35CB088C5AFCA850ADF675CDB5E063412B262A912D0A1E25984BC5FEBFF0194F49A8B388DFD3C5EC02C31062B35D56F04BD1B3F29CE55113785FFAA000778EF5D080E911FF3432187AF0AD7786141429523F274EA749383187A47CF0203010001`|
| 0E | Microsoft Flight Root 2014 | `3082020A0282020100C20F7F6D49BB39F04D943FE8FB4DC5EB3BE1285AB9892A467EA5C333271D82893FEB33A1876AEAE882B9DAC39D77D135C0CB833672A6571912BC15E2C83C7B83623414D5ABB6DE368BA15A71A65196A70633B3221D146253C2A5AF9A40CABE2C485499E72A9368A769190B99693BC1B2ACAE94DC5FAB7E02CADE3CA774A68C10A0E5AEB69C35EF838B10E5972ABA916B9A6A4595D9D054718E653FC48A53CA1E38470AE9D04184A5DA1E66016504E6505B7735F5B42E29320CC6BF5F61EE3220B77C39F911FAFF605EFEC669F46F1E1DED1D06E7651E9A112E6344065F31431733E9A32682D44B83124FD2A126032548E13ABD84F58AD5B46E1AE871200E45530167ADE31E6BE8B2E4ABFDF53B8EBA67AF5984CC5C75D09DAA5C72C42636A2AC324C6AB1F8331744D2A77D70EEEB70949ABCEABA1C104B635B38DDD2254504B2F0B35A7C0B0A8E21406437114D96694533E493839EF9B3B51C2B0571EA6DCCE748B6B6DE805010CA4938B35905704EBD9E880222586489EB40DAB12D2D6A40885D23C33ED0F5D5B7908A28543962A2C5C6B1BF74CD8695F9456BCCF207EAAC5CD336F7A27AB5B472532A063EC337945858B14A71BB5CCD9CB2AF109AD943363E528519E7422891118C8CE7BBDFE6C855087375F3960D86B7D2E506B2C08A54A86177207D6CD1FEBA68F3454AAF1184EB867D2F04F354EA20FFD5DB3D250270870203010001`|
| 0F | Microsoft Third Party Marketplace Root | `3082020A0282020100F0AD5E8240052D682459CBDE0AE884CC48B93B1DB08B52250E1214C410153A84BE81E075E6BA0EF861E36B1DCE9D1EDF9F283336DA8332C8A1A1ED594AE28C600C6A82B19A09A25C222E39ED92F681017AFF91689085A39C8A97837112946E32D71527E6670B7FE57A02FB90FFF049001ACF300C7BFFE94EA806FD2231166DDE496D96AA91261603419B1614EE98B85B4BD3F12FDB7E30FC79A668124A86773CECE533C3DFEA815519AD085E65D3DEAFBD5E741326839CCE585648E08AA76992ED72DB6782C2E6384ECF5F2BA03BD3C38B9A9A17125554A6647394F85356F21DE1BBD9CE92E2275B7DC4569CEB57FC0D9EE4A27A5999BD23C4656C906D08B25E871A6EA7D1F0EA0532857806504996988928566B0D29793567B8629FA3CFEF8563F8BE16DCED94047C6D610F9B78341E824CDD2A1C8F6D80B6DD7A051F84EDD855D711EB8793179F9A4D0E2874AAAC094F0E08BFFE59BF66EEE2F3511C178E3E3E5B7F2478A31CF4CAC2D619FDE8EBED4F94A55F34C49CE254BA48838B6444D3423B156AC60A6810242A227F4BB079D6DEE5E317199098063AEB5981A64EF496233FA28DCC76C8194EBD68553CD8FD8F844439894D1061951AE89CCCAFF14D38AE821C631CBF68EA45A236B6886A042C6BCB66D4C741090DADF3B0B498127369278E60E606ECEE8A6F30E55DDB56F0F02B523CA73B2A1A7EC0FF03C5ECE029DF0203010001`|
| 14 | Microsoft Trusted Root Store | N/A |
| 15 | Microsoft OEM Root Certificate Authority 2017 | `3082020A0282020100F8DB3BE3FCDCEBA78508F59D89CEF3CE3B0FDA78135D682B2FA6977DA8111D685C2CAE4B190FC07E19EC30DA6079E1B9F728EAC5ACFAB79E824700F7015B1BD58112F57A43DCAF44179E179A9D40A8C05BD52F4155144E35C65A40C7D2D6216D4636B678E8311DF6812BC64A05354A5035A1A3783779702E7FB3D48E44B51A71E50F9F0DB4C261A91A664C6F88DC62DCEF19631FB43549D953AC564FAD2C9500C9EDCD351ABB2EFD1DDEFAC282E4CCAE8936D80AA4F28739F1A2E1D5735EA68723962540EAC1850E0619C2867A89584F4FFD372A05B4510BF6122F55A721FFB5B44C609D6160A8453A014F28F1545F78510D322020B06E6FEF9E248173B7D6DA3721C40E674ED45A000B390210BEF3D2C4B5E210144830E3E3049B70429F71A1C8128A333EBA664AF1B216C690D598CFFC160A18D609A2CAAF28BC0DDFE57C81BF0D93A320DAE44FF8E3AB00101D52C4A0049811ECFA872EC5765267A17911AA6D857060F821768C1120CE6FB778C1ED0DA2A3DC3C24B1F371630C174EF80A7EDA331B35A19A87CAA9DCC0DC1889BAF5A1B117899E8C4D70FFDC333ACF78A2BA37BC04A7D376660718B16DD69FE58D0F515680EB16A72E4D4F0233D132C561CFCB2FC0ADE8708AD0A2B50184DB995F8218CF49830367BD7E3A10A72919810D77101BAB42E54A021D45FC048F2C2C3A59A442E3F0E99EA3369537A1AA9D9DA7B90203010001`|
| 16 | Microsoft Identity Verification Root Certificate Authority 2020 | `3082020A0282020100B3912A07830667FD9E9DE0C7C0B7A4E642047F0FA6DB5FFBD55AD745A0FB770BF080F3A66D5A4D7953D8A08684574520C7A254FBC7A2BF8AC76E35F3A215C42F4EE34A8596490DFFBE99D814F6BC2707EE429B2BF50B9206E4FD691365A89172F29884EB833D0EE4D771124821CB0DEDF64749B79BF9C9C717B6844FFFB8AC9AD773674985E386BD3740D02586D4DEB5C26D626AD5A978BC2D6F49F9E56C1414FD14C7D3651637DECB6EBC5E298DFD629B152CD605E6B9893233A362C7D7D6526708C42EF4562B9E0B87CCECA7B4A6AAEB05CD1957A53A0B04271C91679E2D622D2F1EBEDAC020CB0419CA33FB89BE98E272A07235BE79E19C836FE46D176F90F33D008675388ED0E0499ABBDBD3F830CAD55788684D72D3BF6D7F71D8FDBD0DAE926448B75B6F7926B5CD9B952184D1EF0F323D7B578CF345074C7CE05E180E35768B6D9ECB3674AB05F8E0735D3256946797250AC6353D9497E7C1448B80FDC1F8F47419E530F606FB21573E061C8B6B158627497B8293CA59E87547E83F38F4C75379A0B6B4E25C51EFBD5F38C113E6780C955A2EC5405928CC0F24C0ECBA0977239938A6B61CDAC7BA20B6D737D87F37AF08E33B71DB6E731B7D9972B0E486335974B516007B506DC68613DAFDC439823D24009A60DABA94C005512C34AC50991387BBB30580B24D30025CB826835DB46373EFAE23954F6028BE37D55BA50203010001`|

For well-known roots, the TBS hashes for the certificates are baked into the code for App Control for Business. For example, they don't need to be listed as TBS hashes in the policy file.

## Status values

Represents values that are used to communicate system information. They are of four types: success values, information values, warning values, and error values. See [NTSATUS](/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55) for information about common usage details.
