---
title: RemoteRemediation DDF file
description: View the XML file containing the device description framework (DDF) for the RemoteRemediation configuration service provider.
ms.date: 03/26/2025
ms.topic: generated-reference
---

<!-- Auto-Generated CSP Document -->

# RemoteRemediation DDF file

The following XML file contains the device description framework (DDF) for the RemoteRemediation configuration service provider.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE MgmtTree PUBLIC " -//OMA//DTD-DM-DDF 1.2//EN" "http://www.openmobilealliance.org/tech/DTD/DM_DDF-V1_2.dtd"[<?oma-dm-ddf-ver supported-versions="1.2"?>]>
<MgmtTree xmlns:MSFT="http://schemas.microsoft.com/MobileDevice/DM">
  <VerDTD>1.2</VerDTD>
  <MSFT:Diagnostics>
  </MSFT:Diagnostics>
  <Node>
    <NodeName>RemoteRemediation</NodeName>
    <Path>./Vendor/MSFT</Path>
    <DFProperties>
      <AccessType>
        <Get />
      </AccessType>
      <Description>The root node for remote remediation function.</Description>
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
        <MSFT:EditionAllowList>0x4;0x1B;0x30;0x31;0x48;0x54;0x62;0x63;0x64;0x65;0x77;0x79;0x7A;0x7D;0x7E;0x81;0x82;0x87;0x88;0x88*;0x8A;0x8B;0xA1;0xA2;0xA4;0xA5;0xAB;0xAC;0xAF;0xB4;0xBC;0xBD;0xBF;0xCA;0xCB;</MSFT:EditionAllowList>
      </MSFT:Applicability>
    </DFProperties>
    <Node>
      <NodeName>CloudRemediationSettings</NodeName>
      <DFProperties>
        <AccessType>
          <Add />
          <Delete />
          <Get />
          <Replace />
        </AccessType>
        <Description>Interior node containing settings related to cloud remediation. Delete on this node will reset all cloud remediation settings to their default values.</Description>
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
        <MSFT:AtomicRequired />
      </DFProperties>
      <Node>
        <NodeName>EnableCloudRemediation</NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
            <Replace />
          </AccessType>
          <Description>Enable or disable cloud remediation.</Description>
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
              <MSFT:Value>true</MSFT:Value>
              <MSFT:ValueDescription>Cloud remediation enabled</MSFT:ValueDescription>
            </MSFT:Enum>
            <MSFT:Enum>
              <MSFT:Value>false</MSFT:Value>
              <MSFT:ValueDescription>Cloud remediation disabled</MSFT:ValueDescription>
            </MSFT:Enum>
          </MSFT:AllowedValues>
        </DFProperties>
      </Node>
      <Node>
        <NodeName>AutoRemediationSettings</NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
            <Replace />
          </AccessType>
          <Description>Interior node containing settings related to auto remediation. Delete on this node will reset all auto remediation settings to their default values.</Description>
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
          <NodeName>EnableAutoRemediation</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
              <Replace />
            </AccessType>
            <Description>Enable or disable auto remediation.</Description>
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
                <MSFT:Value>true</MSFT:Value>
                <MSFT:ValueDescription>Auto remediation enabled</MSFT:ValueDescription>
              </MSFT:Enum>
              <MSFT:Enum>
                <MSFT:Value>false</MSFT:Value>
                <MSFT:ValueDescription>Auto remediation disabled</MSFT:ValueDescription>
              </MSFT:Enum>
            </MSFT:AllowedValues>
            <MSFT:DependencyBehavior>
              <MSFT:DependencyGroup FriendlyId="EnableCloudRemediation">
                <MSFT:Dependency Type="DependsOn">
                  <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings/EnableCloudRemediation</MSFT:DependencyUri>
                  <MSFT:DependencyAllowedValue ValueType="ENUM">
                    <MSFT:Enum>
                      <MSFT:Value>true</MSFT:Value>
                      <MSFT:ValueDescription>Cloud remediation enabled</MSFT:ValueDescription>
                    </MSFT:Enum>
                  </MSFT:DependencyAllowedValue>
                </MSFT:Dependency>
              </MSFT:DependencyGroup>
            </MSFT:DependencyBehavior>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>SetTimeToReboot</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
              <Replace />
            </AccessType>
            <Description>Get/set the time to reboot (in minutes) during auto cloud remediation. The maximum time to reboot possible is 72 hours. "SetTimeToReboot" is dependent on "EnableAutoRemediation" and only takes effect if "EnableAutoRemediation" is set to true. Otherwise an invalid argument error will be returned and no changes will be made.</Description>
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
              <MSFT:Value>[1-4320]</MSFT:Value>
            </MSFT:AllowedValues>
            <MSFT:DependencyBehavior>
              <MSFT:DependencyGroup FriendlyId="EnableAutoRemediation">
                <MSFT:Dependency Type="DependsOn">
                  <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings/AutoRemediationSettings/EnableAutoRemediation</MSFT:DependencyUri>
                  <MSFT:DependencyAllowedValue ValueType="ENUM">
                    <MSFT:Enum>
                      <MSFT:Value>true</MSFT:Value>
                      <MSFT:ValueDescription>Auto remediation enabled</MSFT:ValueDescription>
                    </MSFT:Enum>
                  </MSFT:DependencyAllowedValue>
                </MSFT:Dependency>
              </MSFT:DependencyGroup>
            </MSFT:DependencyBehavior>
          </DFProperties>
        </Node>
        <Node>
          <NodeName>SetRetryInterval</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
              <Replace />
            </AccessType>
            <Description>Get/set the retry interval (in minutes) during auto cloud remediation. The retry interval should not be higher than the time to reboot. "SetRetryInterval" is dependent on "EnableAutoRemediation" and only takes effect if "EnableAutoRemediation" is set to true. Otherwise, an invalid argument error will be returned and no changes will be made.</Description>
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
              <MSFT:Value>[1,4320]</MSFT:Value>
            </MSFT:AllowedValues>
            <MSFT:DependencyBehavior>
              <MSFT:DependencyGroup FriendlyId="EnableAutoRemediation">
                <MSFT:Dependency Type="DependsOn">
                  <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings/AutoRemediationSettings/EnableAutoRemediation</MSFT:DependencyUri>
                  <MSFT:DependencyAllowedValue ValueType="ENUM">
                    <MSFT:Enum>
                      <MSFT:Value>true</MSFT:Value>
                      <MSFT:ValueDescription>Auto remediation enabled</MSFT:ValueDescription>
                    </MSFT:Enum>
                  </MSFT:DependencyAllowedValue>
                </MSFT:Dependency>
              </MSFT:DependencyGroup>
            </MSFT:DependencyBehavior>
          </DFProperties>
        </Node>
      </Node>
      <Node>
        <NodeName>NetworkSettings</NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
            <Replace />
          </AccessType>
          <Description>Interior node containing settings related to network.</Description>
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
          <NodeName>NetworkCredentials</NodeName>
          <DFProperties>
            <AccessType>
              <Add />
              <Delete />
              <Get />
              <Replace />
            </AccessType>
            <Description>Interior node containing settings related to network credentials.</Description>
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
            <NodeName>NetworkSSID</NodeName>
            <DFProperties>
              <AccessType>
                <Add />
                <Delete />
                <Get />
                <Replace />
              </AccessType>
              <Description>Get/Set the network SSID that cloud remediation will attempt to connect to during remediation.</Description>
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
              <MSFT:AllowedValues ValueType="None">
              </MSFT:AllowedValues>
              <MSFT:DependencyBehavior>
                <MSFT:DependencyGroup FriendlyId="EnableCloudRemediation">
                  <MSFT:Dependency Type="DependsOn">
                    <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings/AutoRemediationSettings/EnableAutoRemediation</MSFT:DependencyUri>
                    <MSFT:DependencyAllowedValue ValueType="ENUM">
                      <MSFT:Enum>
                        <MSFT:Value>true</MSFT:Value>
                        <MSFT:ValueDescription>Cloud remediation enabled</MSFT:ValueDescription>
                      </MSFT:Enum>
                    </MSFT:DependencyAllowedValue>
                  </MSFT:Dependency>
                </MSFT:DependencyGroup>
              </MSFT:DependencyBehavior>
            </DFProperties>
          </Node>
          <Node>
            <NodeName>NetworkPassword</NodeName>
            <DFProperties>
              <AccessType>
                <Add />
                <Delete />
                <Get />
                <Replace />
              </AccessType>
              <Description>Get/Set the password for the wifi network that cloud remediation will attempt to connect during cloud remediation.</Description>
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
              <MSFT:AllowedValues ValueType="None">
              </MSFT:AllowedValues>
              <MSFT:DependencyBehavior>
                <MSFT:DependencyGroup FriendlyId="EnableCloudRemediation">
                  <MSFT:Dependency Type="DependsOn">
                    <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings/AutoRemediationSettings/EnableAutoRemediation</MSFT:DependencyUri>
                    <MSFT:DependencyAllowedValue ValueType="ENUM">
                      <MSFT:Enum>
                        <MSFT:Value>true</MSFT:Value>
                        <MSFT:ValueDescription>Cloud remediation enabled</MSFT:ValueDescription>
                      </MSFT:Enum>
                    </MSFT:DependencyAllowedValue>
                  </MSFT:Dependency>
                </MSFT:DependencyGroup>
              </MSFT:DependencyBehavior>
            </DFProperties>
          </Node>
          <Node>
            <NodeName>NetworkPasswordEncryptionType</NodeName>
            <DFProperties>
              <AccessType>
                <Add />
                <Delete />
                <Get />
                <Replace />
              </AccessType>
              <Description>The type of encryption that might be used for the network password.</Description>
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
              <MSFT:AllowedValues ValueType="ENUM">
                <MSFT:Enum>
                  <MSFT:Value>1</MSFT:Value>
                  <MSFT:ValueDescription>No encryption</MSFT:ValueDescription>
                </MSFT:Enum>
                <MSFT:Enum>
                  <MSFT:Value>2</MSFT:Value>
                  <MSFT:ValueDescription>Encrypt using Mdm certificate</MSFT:ValueDescription>
                </MSFT:Enum>
                <MSFT:Enum>
                  <MSFT:Value>3</MSFT:Value>
                  <MSFT:ValueDescription>Encrypt with custom certificate</MSFT:ValueDescription>
                </MSFT:Enum>
              </MSFT:AllowedValues>
              <MSFT:DependencyBehavior>
                <MSFT:DependencyGroup FriendlyId="EnableCloudRemediation">
                  <MSFT:Dependency Type="DependsOn">
                    <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings//AutoRemediationSettings/EnableAutoRemediation</MSFT:DependencyUri>
                    <MSFT:DependencyAllowedValue ValueType="ENUM">
                      <MSFT:Enum>
                        <MSFT:Value>true</MSFT:Value>
                        <MSFT:ValueDescription>Cloud remediation enabled</MSFT:ValueDescription>
                      </MSFT:Enum>
                    </MSFT:DependencyAllowedValue>
                  </MSFT:Dependency>
                </MSFT:DependencyGroup>
              </MSFT:DependencyBehavior>
            </DFProperties>
          </Node>
          <Node>
            <NodeName>NetworkPasswordEncryptionStore</NodeName>
            <DFProperties>
              <AccessType>
                <Add />
                <Delete />
                <Get />
                <Replace />
              </AccessType>
              <Description>The encryption store that is specified if we are using a custom certificate for password encryption.</Description>
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
              <MSFT:AllowedValues ValueType="None">
              </MSFT:AllowedValues>
              <MSFT:DependencyBehavior>
                <MSFT:DependencyGroup FriendlyId="EnableCloudRemediation">
                  <MSFT:Dependency Type="DependsOn">
                    <MSFT:DependencyUri>Vendor/MSFT/RemoteRemediation/CloudRemediationSettings//AutoRemediationSettings/EnableAutoRemediation</MSFT:DependencyUri>
                    <MSFT:DependencyAllowedValue ValueType="ENUM">
                      <MSFT:Enum>
                        <MSFT:Value>true</MSFT:Value>
                        <MSFT:ValueDescription>Cloud remediation enabled</MSFT:ValueDescription>
                      </MSFT:Enum>
                    </MSFT:DependencyAllowedValue>
                  </MSFT:Dependency>
                </MSFT:DependencyGroup>
              </MSFT:DependencyBehavior>
            </DFProperties>
          </Node>
        </Node>
      </Node>
    </Node>
  </Node>
</MgmtTree>
```

## Related articles

[RemoteRemediation configuration service provider reference](remoteremediation-csp.md)
