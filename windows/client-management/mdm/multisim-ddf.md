---
title: MultiSIM DDF file
description: View the XML file containing the device description framework (DDF) for the MultiSIM configuration service provider.
ms.date: 06/09/2025
ms.topic: generated-reference
---

<!-- Auto-Generated CSP Document -->

# MultiSIM DDF file

The following XML file contains the device description framework (DDF) for the MultiSIM configuration service provider.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE MgmtTree PUBLIC " -//OMA//DTD-DM-DDF 1.2//EN" "http://www.openmobilealliance.org/tech/DTD/DM_DDF-V1_2.dtd"[<?oma-dm-ddf-ver supported-versions="1.2"?>]>
<MgmtTree xmlns:MSFT="http://schemas.microsoft.com/MobileDevice/DM">
  <VerDTD>1.2</VerDTD>
  <MSFT:Diagnostics>
  </MSFT:Diagnostics>
  <Node>
    <NodeName>MultiSIM</NodeName>
    <Path>./Device/Vendor/MSFT</Path>
    <DFProperties>
      <AccessType>
        <Get />
      </AccessType>
      <Description>Subtree for multi-SIM management.</Description>
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
        <MIME />
      </DFType>
      <MSFT:Applicability>
        <MSFT:OsBuildVersion>10.0.17134</MSFT:OsBuildVersion>
        <MSFT:CspVersion>1.0</MSFT:CspVersion>
        <MSFT:EditionAllowList>0x4;0x1B;0x30;0x31;0x48;0x54;0x79;0x7A;0x7D;0x7E;0x81;0x82;0x8A;0x8B;0xA1;0xA2;0xA4;0xA5;0xAB;0xAC;0xAF;0xBC;0xBF;0xCA;0xCB;0xCD;0xCF;</MSFT:EditionAllowList>
      </MSFT:Applicability>
    </DFProperties>
    <Node>
      <NodeName>
      </NodeName>
      <DFProperties>
        <AccessType>
          <Get />
        </AccessType>
        <Description>Node representing a Mobile Broadband Modem. The node name is the Modem ID. Modem ID is a GUID without curly braces, with exception of "Embedded" which represents the embedded Modem.</Description>
        <DFFormat>
          <node />
        </DFFormat>
        <Occurrence>
          <ZeroOrMore />
        </Occurrence>
        <Scope>
          <Dynamic />
        </Scope>
        <DFTitle>ModemID</DFTitle>
        <DFType>
          <DDFName />
        </DFType>
        <MSFT:DynamicNodeNaming>
          <MSFT:UniqueName>The Modem ID associated with the device.</MSFT:UniqueName>
        </MSFT:DynamicNodeNaming>
      </DFProperties>
      <Node>
        <NodeName>Identifier</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Modem ID.</Description>
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
        </DFProperties>
      </Node>
      <Node>
        <NodeName>IsEmbedded</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Indicates whether this Modem is embedded or external.</Description>
          <DFFormat>
            <bool />
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
        </DFProperties>
      </Node>
      <Node>
        <NodeName>Slots</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Represents all SIM slots in the Modem.</Description>
          <DFFormat>
            <node />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Dynamic />
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
              <Get />
            </AccessType>
            <Description>Node representing a SIM Slot. The node name is the Slot ID. SIM Slot ID format is "0", "1", etc., with exception of "Embedded" which represents the embedded Slot.</Description>
            <DFFormat>
              <node />
            </DFFormat>
            <Occurrence>
              <ZeroOrMore />
            </Occurrence>
            <Scope>
              <Dynamic />
            </Scope>
            <DFTitle>SlotID</DFTitle>
            <DFType>
              <DDFName />
            </DFType>
            <MSFT:DynamicNodeNaming>
              <MSFT:UniqueName>The SIM slot ID.</MSFT:UniqueName>
            </MSFT:DynamicNodeNaming>
          </DFProperties>
          <Node>
            <NodeName>Identifier</NodeName>
            <DFProperties>
              <AccessType>
                <Get />
              </AccessType>
              <Description>Slot ID.</Description>
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
            </DFProperties>
          </Node>
          <Node>
            <NodeName>IsEmbedded</NodeName>
            <DFProperties>
              <AccessType>
                <Get />
              </AccessType>
              <Description>Indicates whether this Slot is embedded or a physical SIM slot.</Description>
              <DFFormat>
                <bool />
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
            </DFProperties>
          </Node>
          <Node>
            <NodeName>IsSelected</NodeName>
            <DFProperties>
              <AccessType>
                <Get />
                <Replace />
              </AccessType>
              <Description>Indicates whether this Slot is selected or not.</Description>
              <DFFormat>
                <bool />
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
                  <MSFT:Value>false</MSFT:Value>
                  <MSFT:ValueDescription>Not selected</MSFT:ValueDescription>
                </MSFT:Enum>
                <MSFT:Enum>
                  <MSFT:Value>true</MSFT:Value>
                  <MSFT:ValueDescription>Selected</MSFT:ValueDescription>
                </MSFT:Enum>
              </MSFT:AllowedValues>
            </DFProperties>
          </Node>
          <Node>
            <NodeName>State</NodeName>
            <DFProperties>
              <AccessType>
                <Get />
              </AccessType>
              <Description>Slot state (Unknown = 0, OffEmpty = 1, Off = 2, Empty = 3, NotReady = 4, Active = 5, Error = 6, ActiveEsim = 7, ActiveEsimNoProfile = 8)</Description>
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
            </DFProperties>
          </Node>
        </Node>
      </Node>
      <Node>
        <NodeName>Policies</NodeName>
        <DFProperties>
          <AccessType>
            <Get />
          </AccessType>
          <Description>Policies associated with the Modem.</Description>
          <DFFormat>
            <node />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Dynamic />
          </Scope>
          <DFType>
            <DDFName />
          </DFType>
        </DFProperties>
        <Node>
          <NodeName>SlotSelectionEnabled</NodeName>
          <DFProperties>
            <AccessType>
              <Get />
              <Replace />
            </AccessType>
            <DefaultValue>true</DefaultValue>
            <Description>Determines whether the user is allowed to change slots in the Cellular settings UI. Default is true.</Description>
            <DFFormat>
              <bool />
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
                <MSFT:Value>false</MSFT:Value>
                <MSFT:ValueDescription>Disabled</MSFT:ValueDescription>
              </MSFT:Enum>
              <MSFT:Enum>
                <MSFT:Value>true</MSFT:Value>
                <MSFT:ValueDescription>Enabled</MSFT:ValueDescription>
              </MSFT:Enum>
            </MSFT:AllowedValues>
          </DFProperties>
        </Node>
      </Node>
    </Node>
  </Node>
</MgmtTree>
```

## Related articles

[MultiSIM configuration service provider reference](multisim-csp.md)
