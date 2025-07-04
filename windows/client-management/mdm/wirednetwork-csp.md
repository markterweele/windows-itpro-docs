---
title: WiredNetwork CSP
description: Learn more about the WiredNetwork CSP.
ms.date: 06/10/2025
ms.topic: generated-reference
---

<!-- Auto-Generated CSP Document -->

<!-- WiredNetwork-Begin -->
# WiredNetwork CSP

<!-- WiredNetwork-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
The WiredNetwork configuration service provider (CSP) is used by the enterprise to configure wired Internet on devices that don't have group policy to enable them to access corporate Internet over ethernet.
<!-- WiredNetwork-Editable-End -->

<!-- WiredNetwork-Tree-Begin -->
The following list shows the WiredNetwork configuration service provider nodes:

- ./Device/Vendor/MSFT/WiredNetwork
  - [EnableBlockPeriod](#deviceenableblockperiod)
  - [LanXML](#devicelanxml)
- ./User/Vendor/MSFT/WiredNetwork
  - [EnableBlockPeriod](#userenableblockperiod)
  - [LanXML](#userlanxml)
<!-- WiredNetwork-Tree-End -->

<!-- Device-EnableBlockPeriod-Begin -->
## Device/EnableBlockPeriod

<!-- Device-EnableBlockPeriod-Applicability-Begin -->
| Scope | Editions | Applicable OS |
|:--|:--|:--|
| ✅ Device <br> ✅ User | ✅ Pro <br> ✅ Enterprise <br> ✅ Education <br> ✅ IoT Enterprise / IoT Enterprise LTSC | ✅ Windows 10, version 1809 [10.0.17763] and later |
<!-- Device-EnableBlockPeriod-Applicability-End -->

<!-- Device-EnableBlockPeriod-OmaUri-Begin -->
```Device
./Device/Vendor/MSFT/WiredNetwork/EnableBlockPeriod
```
<!-- Device-EnableBlockPeriod-OmaUri-End -->

<!-- Device-EnableBlockPeriod-Description-Begin -->
<!-- Description-Source-DDF -->
Enable block period (minutes), used to specify the duration for which automatic authentication attempts will be blocked from occurring after a failed authentication attempt.
<!-- Device-EnableBlockPeriod-Description-End -->

<!-- Device-EnableBlockPeriod-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
<!-- Device-EnableBlockPeriod-Editable-End -->

<!-- Device-EnableBlockPeriod-DFProperties-Begin -->
**Description framework properties**:

| Property name | Property value |
|:--|:--|
| Format | `int` |
| Access Type | Add, Delete, Get, Replace |
| Allowed Values | Range: `[0-4294967295]` |
<!-- Device-EnableBlockPeriod-DFProperties-End -->

<!-- Device-EnableBlockPeriod-Examples-Begin -->
<!-- Add any examples for this policy here. Examples outside this section will get overwritten. -->
<!-- Device-EnableBlockPeriod-Examples-End -->

<!-- Device-EnableBlockPeriod-End -->

<!-- Device-LanXML-Begin -->
## Device/LanXML

<!-- Device-LanXML-Applicability-Begin -->
| Scope | Editions | Applicable OS |
|:--|:--|:--|
| ✅ Device <br> ✅ User | ✅ Pro <br> ✅ Enterprise <br> ✅ Education <br> ✅ IoT Enterprise / IoT Enterprise LTSC | ✅ Windows 10, version 1809 [10.0.17763] and later |
<!-- Device-LanXML-Applicability-End -->

<!-- Device-LanXML-OmaUri-Begin -->
```Device
./Device/Vendor/MSFT/WiredNetwork/LanXML
```
<!-- Device-LanXML-OmaUri-End -->

<!-- Device-LanXML-Description-Begin -->
<!-- Description-Source-DDF -->
XML describing the wired network configuration and follows the LAN_profile schemas <https://msdn.microsoft.com/library/windows/desktop/aa816366(v=vs.85).aspx>
<!-- Device-LanXML-Description-End -->

<!-- Device-LanXML-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
The profile XML must be escaped, as shown in the following examples.

> [!NOTE]
> If you need to specify other advanced conditions, such as specifying criteria for certificates that can be used by the LAN profile, you can do so by specifying this through the [EapHostConfig](/windows/win32/eaphost/eaphostconfigschema-eaphostconfig-element) portion of the LanXML ([LANProfile](/windows/win32/nativewifi/lan-profileschema-schema) > [MSM](/windows/win32/nativewifi/lan-profileschema-msm-lanprofile-element) > [security](/windows/win32/nativewifi/lan-profileschema-security-msm-element) > [OneX](/windows/win32/nativewifi/onexschema-onex-element) > EAPConfig). For more information, see [EAP configuration](./eap-configuration.md) and [Extensible Authentication Protocol (EAP) for network access](/windows-server/networking/technologies/extensible-authentication-protocol/network-access). For an example, see [Wired Profile Samples](/windows/win32/nativewifi/wired-profile-samples).
<!-- Device-LanXML-Editable-End -->

<!-- Device-LanXML-DFProperties-Begin -->
**Description framework properties**:

| Property name | Property value |
|:--|:--|
| Format | `chr` (string) |
| Access Type | Add, Delete, Get, Replace |
<!-- Device-LanXML-DFProperties-End -->

<!-- Device-LanXML-Examples-Begin -->
<!-- Add any examples for this policy here. Examples outside this section will get overwritten. -->
See [Examples](#examples).
<!-- Device-LanXML-Examples-End -->

<!-- Device-LanXML-End -->

<!-- User-EnableBlockPeriod-Begin -->
## User/EnableBlockPeriod

<!-- User-EnableBlockPeriod-Applicability-Begin -->
| Scope | Editions | Applicable OS |
|:--|:--|:--|
| ✅ Device <br> ✅ User | ✅ Pro <br> ✅ Enterprise <br> ✅ Education <br> ✅ IoT Enterprise / IoT Enterprise LTSC | ✅ Windows 10, version 1809 [10.0.17763] and later |
<!-- User-EnableBlockPeriod-Applicability-End -->

<!-- User-EnableBlockPeriod-OmaUri-Begin -->
```User
./User/Vendor/MSFT/WiredNetwork/EnableBlockPeriod
```
<!-- User-EnableBlockPeriod-OmaUri-End -->

<!-- User-EnableBlockPeriod-Description-Begin -->
<!-- Description-Source-DDF -->
Enable block period (minutes), used to specify the duration for which automatic authentication attempts will be blocked from occurring after a failed authentication attempt.
<!-- User-EnableBlockPeriod-Description-End -->

<!-- User-EnableBlockPeriod-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
<!-- User-EnableBlockPeriod-Editable-End -->

<!-- User-EnableBlockPeriod-DFProperties-Begin -->
**Description framework properties**:

| Property name | Property value |
|:--|:--|
| Format | `int` |
| Access Type | Add, Delete, Get, Replace |
| Allowed Values | Range: `[0-4294967295]` |
<!-- User-EnableBlockPeriod-DFProperties-End -->

<!-- User-EnableBlockPeriod-Examples-Begin -->
<!-- Add any examples for this policy here. Examples outside this section will get overwritten. -->
<!-- User-EnableBlockPeriod-Examples-End -->

<!-- User-EnableBlockPeriod-End -->

<!-- User-LanXML-Begin -->
## User/LanXML

<!-- User-LanXML-Applicability-Begin -->
| Scope | Editions | Applicable OS |
|:--|:--|:--|
| ✅ Device <br> ✅ User | ✅ Pro <br> ✅ Enterprise <br> ✅ Education <br> ✅ IoT Enterprise / IoT Enterprise LTSC | ✅ Windows 10, version 1809 [10.0.17763] and later |
<!-- User-LanXML-Applicability-End -->

<!-- User-LanXML-OmaUri-Begin -->
```User
./User/Vendor/MSFT/WiredNetwork/LanXML
```
<!-- User-LanXML-OmaUri-End -->

<!-- User-LanXML-Description-Begin -->
<!-- Description-Source-DDF -->
XML describing the wired network configuration and follows the LAN_profile schemas <https://msdn.microsoft.com/library/windows/desktop/aa816366(v=vs.85).aspx>
<!-- User-LanXML-Description-End -->

<!-- User-LanXML-Editable-Begin -->
<!-- Add any additional information about this policy here. Anything outside this section will get overwritten. -->
For more information, see [Device/LanXML](#devicelanxml).
<!-- User-LanXML-Editable-End -->

<!-- User-LanXML-DFProperties-Begin -->
**Description framework properties**:

| Property name | Property value |
|:--|:--|
| Format | `chr` (string) |
| Access Type | Add, Delete, Get, Replace |
<!-- User-LanXML-DFProperties-End -->

<!-- User-LanXML-Examples-Begin -->
<!-- Add any examples for this policy here. Examples outside this section will get overwritten. -->
<!-- User-LanXML-Examples-End -->

<!-- User-LanXML-End -->

<!-- WiredNetwork-CspMoreInfo-Begin -->
<!-- Add any additional information about this CSP here. Anything outside this section will get overwritten. -->
## Examples

The following example shows how to add a wired network profile that authenticates with PEAP-MSCHAPv2. This example is based on the sample profile at [PEAP Profile Sample](/windows/win32/nativewifi/peap-profile-sample)

```xml
<SyncML xmlns="SYNCML:SYNCML1.2">
  <SyncBody>
    <Add>
      <CmdID>1</CmdID>
      <Item>
        <Target>
          <LocURI>./Device/Vendor/MSFT/WiredNetwork/LanXML</LocURI>
        </Target>
        <Meta>
          <Format xmlns="syncml:metinf">chr</Format>
        </Meta>
        <Data><![CDATA[<?xml version="1.0"?><LANProfile xmlns="http://www.microsoft.com/networking/LAN/profile/v1"><MSM><security><OneXEnforced>false</OneXEnforced><OneXEnabled>true</OneXEnabled><OneX xmlns="http://www.microsoft.com/networking/OneX/v1"><EAPConfig><EapHostConfig xmlns="http://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="http://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>false</DisableUserPromptForServerValidation><ServerNames></ServerNames></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>26</Type><EapType xmlns="http://www.microsoft.com/provisioning/MsChapV2ConnectionPropertiesV1"><UseWinLogonCredentials>false</UseWinLogonCredentials></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">false</AcceptServerName><PeapExtensionsV2 xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"><AllowPromptingWhenServerCANotFound xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV3">true</AllowPromptingWhenServerCANotFound></PeapExtensionsV2></PeapExtensions></EapType></Eap></Config></EapHostConfig></EAPConfig></OneX></security></MSM></LANProfile>]]></Data>
      </Item>
    </Add>
  </SyncBody>
</SyncML>
```
<!-- WiredNetwork-CspMoreInfo-End -->

<!-- WiredNetwork-End -->

## Related articles

- [Wired profile samples](/windows/win32/nativewifi/wired-profile-samples)
- [Configuration service provider reference](configuration-service-provider-reference.md)
- [Extensible Authentication Protocol (EAP) for network access](/windows-server/networking/technologies/extensible-authentication-protocol/network-access)
- [Configure EAP profiles and settings in Windows](/windows-server/networking/technologies/extensible-authentication-protocol/configure-eap-profiles)
