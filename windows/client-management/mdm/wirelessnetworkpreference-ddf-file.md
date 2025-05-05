---
title: WirelessNetworkPreference DDF file
description: View the XML file containing the device description framework (DDF) for the WirelessNetworkPreference configuration service provider.
ms.date: 04/30/2025
ms.topic: generated-reference
---

<!-- Auto-Generated CSP Document -->

# WirelessNetworkPreference DDF file

The following XML file contains the device description framework (DDF) for the WirelessNetworkPreference configuration service provider.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE MgmtTree PUBLIC " -//OMA//DTD-DM-DDF 1.2//EN" "http://www.openmobilealliance.org/tech/DTD/DM_DDF-V1_2.dtd"[<?oma-dm-ddf-ver supported-versions="1.2"?>]>
<MgmtTree xmlns:MSFT="http://schemas.microsoft.com/MobileDevice/DM">
  <VerDTD>1.2</VerDTD>
  <MSFT:Diagnostics>
  </MSFT:Diagnostics>
  <Node>
    <NodeName>WirelessNetworkPreference</NodeName>
    <Path>./Device/Vendor/MSFT</Path>
    <DFProperties>
      <AccessType>
        <Get />
      </AccessType>
      <Description>Represents information associated with wireless networks prioritization including detailed connectivity priorities for specific cellular networks with a unique PLMN ID.</Description>
      <DFFormat>
        <node />
      </DFFormat>
      <Occurrence>
        <One />
      </Occurrence>
      <Scope>
        <Permanent />
      </Scope>
      <DFType>
        <DDFName />
      </DFType>
      <MSFT:Applicability>
        <MSFT:OsBuildVersion>99.9.99999</MSFT:OsBuildVersion>
        <MSFT:CspVersion>1.0</MSFT:CspVersion>
        <MSFT:EditionAllowList>0x4;0x1B;0x30;0x31;0x48;0x54;0x62;0x63;0x64;0x65;0x79;0x7A;0x7D;0x7E;0x81;0x82;0x88;0x8A;0x8B;0xA1;0xA2;0xA4;0xA5;0xAB;0xAC;0xAF;0xBC;0xBF;0xCA;0xCB;0xCD;0xCF;0xD2;</MSFT:EditionAllowList>
      </MSFT:Applicability>
    </DFProperties>
    <Node>
      <NodeName>IsEnabled</NodeName>
      <DFProperties>
        <AccessType>
          <Get />
          <Replace />
        </AccessType>
        <DefaultValue>False</DefaultValue>
        <Description>It determines whether the wireless connectivity management policy is enabled or not.</Description>
        <DFFormat>
          <bool />
        </DFFormat>
        <Occurrence>
          <One />
        </Occurrence>
        <Scope>
          <Permanent />
        </Scope>
        <DFType>
          <MIME />
        </DFType>
        <MSFT:AllowedValues ValueType="ENUM">
          <MSFT:Enum>
            <MSFT:Value>False</MSFT:Value>
            <MSFT:ValueDescription>Disable the wireless management policy.</MSFT:ValueDescription>
          </MSFT:Enum>
          <MSFT:Enum>
            <MSFT:Value>True</MSFT:Value>
            <MSFT:ValueDescription>Enable the wireless management policy.</MSFT:ValueDescription>
          </MSFT:Enum>
        </MSFT:AllowedValues>
      </DFProperties>
    </Node>
    <Node>
      <NodeName>PreferCellularOverWiFi</NodeName>
      <DFProperties>
        <AccessType>
          <Get />
          <Replace />
        </AccessType>
        <DefaultValue>False</DefaultValue>
        <Description>It determines the order of preference between Wi-Fi and cellular networks. When the value is set to “False”, Wi-Fi is preferred over cellular. When the value is set to “True”, cellular is preferred over Wi-Fi. </Description>
        <DFFormat>
          <bool />
        </DFFormat>
        <Occurrence>
          <One />
        </Occurrence>
        <Scope>
          <Permanent />
        </Scope>
        <DFType>
          <MIME />
        </DFType>
        <MSFT:AllowedValues ValueType="ENUM">
          <MSFT:Enum>
            <MSFT:Value>False</MSFT:Value>
            <MSFT:ValueDescription>Prefer Wi-Fi over Cellular.</MSFT:ValueDescription>
          </MSFT:Enum>
          <MSFT:Enum>
            <MSFT:Value>True</MSFT:Value>
            <MSFT:ValueDescription>Prefer Cellular over Wi-Fi.</MSFT:ValueDescription>
          </MSFT:Enum>
        </MSFT:AllowedValues>
      </DFProperties>
    </Node>
    <Node>
      <NodeName>Status</NodeName>
      <DFProperties>
        <AccessType>
          <Get />
        </AccessType>
        <Description>Nodes that indicate the status of the wireless connectivity management service.</Description>
        <DFFormat>
          <node />
        </DFFormat>
        <Occurrence>
          <One />
        </Occurrence>
        <Scope>
          <Permanent />
        </Scope>
        <DFType>
          <DDFName />
        </DFType>
      </DFProperties>
      <Node>
        <NodeName>eSIMprofilesCount</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Count of operational eSIM profiles stored in the eUICC.</Description>
          <DFFormat>
            <int />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Permanent />
          </Scope>
          <DFType>
            <MIME />
          </DFType>
        </DFProperties>
      </Node>
      <Node>
        <NodeName>eSIMprofilesMatched</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Count of operational eSIM profiles stored on the eUICC whose PLMN ID matches one of the ConnectionProfileIDs setup under the ConnectionProfiles node. Only matched profiles with no errors will be counted. If more than one eSIM profile with the same PLMN ID is configured on the policy and/or more than one eSIM profile with the same PLMN ID is stored in the eUICC, then they will not be counted even if there is a match.</Description>
          <DFFormat>
            <int />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Permanent />
          </Scope>
          <DFType>
            <MIME />
          </DFType>
        </DFProperties>
      </Node>
      <Node>
        <NodeName>eSIMpolicyStatus</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>An integer indicating the current status of the wireless connectivity management service. If the value is zero, there are no errors. \n\n 0 = No errors. \n 1 = No policies are configured. \n 2 = More than one policy has the same priority. \n 3 = More than one policy references the same PLMN ID. \n 4 = Invalid PLMN ID for one or more of the configured profiles. \n 5 = More than one eSIM profile stored in the eUICC with the same PLMN ID. \n 6 = Invalid configuration value for one or more of the cellular parameters. Please review CSP documentation. \n\n Warning: Any of these errors will result in a complete halt of the wireless connectivity management service.</Description>
          <DFFormat>
            <int />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Permanent />
          </Scope>
          <DFType>
            <MIME />
          </DFType>
        </DFProperties>
      </Node>
    </Node>
    <Node>
      <NodeName>Parameters</NodeName>
      <DFProperties>
        <AccessType>
          <Get />
        </AccessType>
        <Description>Parameters to configure the behavior of the wireless connectivity management service.</Description>
        <DFFormat>
          <node />
        </DFFormat>
        <Occurrence>
          <One />
        </Occurrence>
        <Scope>
          <Permanent />
        </Scope>
        <DFType>
          <DDFName />
        </DFType>
      </DFProperties>
      <Node>
        <NodeName>CellularParameters</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Parameters to configure the cellular-specific behavior of the wireless connectivity management service.</Description>
          <DFFormat>
            <node />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Permanent />
          </Scope>
          <DFType>
            <DDFName />
          </DFType>
        </DFProperties>
        <Node>
          <NodeName>NetworkDiscoveryOption</NodeName>
          <DFProperties>
            <AccessType>
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>0</DefaultValue>
            <Description>Configures which approach should be used in the network discovery process. There are two possible values: (0) no network scan will be performed – rather, registration and connection will be attempted with each eSIM profile in descending order of preference; or (1) Network scan will be performed using the current active eSIM profile. This option works for modems that when performing a network scan show the complete list of available networks independently of which eSIM profile is active.</Description>
            <DFFormat>
              <int />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Permanent />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="ENUM">
              <MSFT:Enum>
                <MSFT:Value>0</MSFT:Value>
                <MSFT:ValueDescription>No network scan will be performed -- rather, registration and connection will be attempted with each eSIM profile in descending order of preference.</MSFT:ValueDescription>
              </MSFT:Enum>
              <MSFT:Enum>
                <MSFT:Value>1</MSFT:Value>
                <MSFT:ValueDescription>Network scan will be performed using the current active eSIM profile.</MSFT:ValueDescription>
              </MSFT:Enum>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>MaxRescanIntervalInSeconds</NodeName>
          <DFProperties>
            <AccessType>
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>0</DefaultValue>
            <Description>Maximum time (in seconds) from the point that no connection could be established using the permissible eSIM profiles on the device to the start of the next round of network discovery attempts. A smaller interval increases network discovery frequency and can decrease battery life significantly. A value of 0 means that the device is to pick a reasonable interval per its own discretion.</Description>
            <DFFormat>
              <int />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Permanent />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="Range">
              <MSFT:Value>[0-360]</MSFT:Value>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>PreferredProfileWakeConnectionTimerInSeconds</NodeName>
          <DFProperties>
            <AccessType>
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>200</DefaultValue>
            <Description>When the device is woken from sleep with the most-preferred profile already enabled, this value configures the amount of time (in seconds) before the agent will give up on waiting for connection re-establishment with the most-preferred profile and start network discovery.</Description>
            <DFFormat>
              <int />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Permanent />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="Range">
              <MSFT:Value>[30-360]</MSFT:Value>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>ProfileRegistrationTimerInSeconds</NodeName>
          <DFProperties>
            <AccessType>
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>30</DefaultValue>
            <Description>When evaluating eSIM profiles for connectivity, this value configures the amount of time (in seconds) that the agent will wait for network registration before considering this profile unsatisfactory and moving on to the next one.</Description>
            <DFFormat>
              <int />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Permanent />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="Range">
              <MSFT:Value>[20-360]</MSFT:Value>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>ScreenOffDurationToTriggerNetworkDiscoveryInMinutes</NodeName>
          <DFProperties>
            <AccessType>
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>10</DefaultValue>
            <Description>When the device experiences screen off and back on, this value configures the minimum duration (in minutes) of the screen off period that will trigger network discovery.</Description>
            <DFFormat>
              <int />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Permanent />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="Range">
              <MSFT:Value>[0-30]</MSFT:Value>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
      </Node>
    </Node>
    <Node>
      <NodeName>ConnectionProfiles</NodeName>
      <DFProperties>
        <AccessType>
          <Get />
        </AccessType>
        <Description>Profiles to connect to wireless networks in a specified priority order.</Description>
        <DFFormat>
          <node />
        </DFFormat>
        <Occurrence>
          <One />
        </Occurrence>
        <Scope>
          <Permanent />
        </Scope>
        <DFType>
          <DDFName />
        </DFType>
      </DFProperties>
      <Node>
        <NodeName>
        </NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
          </AccessType>
          <Description>Unique identifier of a network preference policy. Unique ID is auto-generated.</Description>
          <DFFormat>
            <node />
          </DFFormat>
          <Occurrence>
            <ZeroOrMore />
          </Occurrence>
          <Scope>
            <Dynamic />
          </Scope>
          <DFTitle>ConnectionProfileID</DFTitle>
          <DFType>
            <DDFName />
          </DFType>
          <MSFT:DynamicNodeNaming>
            <MSFT:ServerGeneratedUniqueIdentifier />
          </MSFT:DynamicNodeNaming>
        </DFProperties>
        <Node>
          <NodeName>Priority</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
              <Replace />
            </AccessType>
            <Description>Priority of a policy compared to the others where 1 represents the highest priority. Thus, the smaller this value is, the higher preference this specific network will receive in establishing a data connection. </Description>
            <DFFormat>
              <int />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Dynamic />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="Range">
              <MSFT:Value>[1-2147483647]</MSFT:Value>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>WirelessType</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>0</DefaultValue>
            <Description>Type of wireless network (either Cellular or Wi-Fi). 0 represents Cellular, and 1 represents Wi-Fi. Currently only cellular is supported.</Description>
            <DFFormat>
              <bin />
            </DFFormat>
            <Occurrence>
              <One />
            </Occurrence>
            <Scope>
              <Dynamic />
            </Scope>
            <DFType>
              <MIME />
            </DFType>
            <MSFT:AllowedValues ValueType="ENUM">
              <MSFT:Enum>
                <MSFT:Value>0</MSFT:Value>
                <MSFT:ValueDescription>Cellular</MSFT:ValueDescription>
              </MSFT:Enum>
              <MSFT:Enum>
                <MSFT:Value>1</MSFT:Value>
                <MSFT:ValueDescription>Wi-Fi</MSFT:ValueDescription>
              </MSFT:Enum>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>Cellular</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
            </AccessType>
            <Description>Identifiers for cellular networks.</Description>
            <DFFormat>
              <node />
            </DFFormat>
            <Occurrence>
              <ZeroOrOne />
            </Occurrence>
            <Scope>
              <Dynamic />
            </Scope>
            <DFType>
              <DDFName />
            </DFType>
          </DFProperties>
          <Node>
            <NodeName>PLMNID</NodeName>
            <DFProperties>
              <AccessType>
                <Add />
                <Delete />
                <Get />
                <Replace />
              </AccessType>
              <Description>5- or 6-digit string identifying a cellular network. It consists of the combination of Mobile Country Code (MCC) and Mobile Network Code (MNC). </Description>
              <DFFormat>
                <chr />
              </DFFormat>
              <Occurrence>
                <One />
              </Occurrence>
              <Scope>
                <Dynamic />
              </Scope>
              <DFType>
                <MIME />
              </DFType>
              <MSFT:AllowedValues ValueType="RegEx">
                <MSFT:Value>^[0-9]{5,6}$</MSFT:Value>
              </MSFT:AllowedValues>
            </DFProperties>
          </Node>
        </Node>
      </Node>
    </Node>
  </Node>
</MgmtTree>
```

## Related articles

[WirelessNetworkPreference configuration service provider reference](wirelessnetworkpreference-csp.md)
