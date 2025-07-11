---
title: Reboot DDF file
description: View the XML file containing the device description framework (DDF) for the Reboot configuration service provider.
ms.date: 04/04/2025
ms.topic: generated-reference
---

<!-- Auto-Generated CSP Document -->

# Reboot DDF file

The following XML file contains the device description framework (DDF) for the Reboot configuration service provider.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE MgmtTree PUBLIC " -//OMA//DTD-DM-DDF 1.2//EN" "http://www.openmobilealliance.org/tech/DTD/DM_DDF-V1_2.dtd"[<?oma-dm-ddf-ver supported-versions="1.2"?>]>
<MgmtTree xmlns:MSFT="http://schemas.microsoft.com/MobileDevice/DM">
  <VerDTD>1.2</VerDTD>
  <MSFT:Diagnostics>
  </MSFT:Diagnostics>
  <Node>
    <NodeName>Reboot</NodeName>
    <Path>./Device/Vendor/MSFT</Path>
    <DFProperties>
      <AccessType>
        <Get />
      </AccessType>
      <Description>The root node for the Reboot configuration service provider.</Description>
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
        <MSFT:OsBuildVersion>10.0.14393</MSFT:OsBuildVersion>
        <MSFT:CspVersion>1.0</MSFT:CspVersion>
        <MSFT:EditionAllowList>0x4;0x1B;0x30;0x31;0x48;0x54;0x79;0x7A;0x7D;0x7E;0x81;0x82;0x88;0x8A;0x8B;0xA1;0xA2;0xA4;0xA5;0xAB;0xAC;0xAF;0xBC;0xBF;0xCA;0xCB;0xCD;0xCF;0xD2;</MSFT:EditionAllowList>
      </MSFT:Applicability>
    </DFProperties>
    <Node>
      <NodeName>RebootNow</NodeName>
      <DFProperties>
        <AccessType>
          <Exec />
          <Get />
        </AccessType>
        <Description>This node executes a reboot of the device. RebootNow triggers a reboot within 5 minutes to allow the user to wrap up any active work. If this node is set to execute during a sync session, the device will reboot at the end of the sync session.</Description>
        <DFFormat>
          <null />
        </DFFormat>
        <Occurrence>
          <One />
        </Occurrence>
        <Scope>
          <Permanent />
        </Scope>
        <DFTitle>RebootNow</DFTitle>
        <DFType>
          <MIME />
        </DFType>
      </DFProperties>
    </Node>
    <Node>
      <NodeName>Schedule</NodeName>
      <DFProperties>
        <AccessType>
          <Get />
        </AccessType>
        <Description>The supported operation is Get.</Description>
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
        <NodeName>Single</NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
            <Replace />
          </AccessType>
          <Description>Value in ISO8601 date and time format (such as 2025-10-07T10:35:00) is required.  Both the date and time are required. A reboot will be scheduled to occur at the specified date and time. Setting a null (empty) date will delete the existing schedule.</Description>
          <DFFormat>
            <chr />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Dynamic />
          </Scope>
          <DFTitle>Single</DFTitle>
          <DFType>
            <MIME />
          </DFType>
          <MSFT:AllowedValues ValueType="None">
          </MSFT:AllowedValues>
        </DFProperties>
      </Node>
      <Node>
        <NodeName>DailyRecurrent</NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
            <Replace />
          </AccessType>
          <Description>Value in ISO8601 date and time format (such as 2025-10-07T10:35:00) is required.  While it is supported to set either DailyRecurrent or WeeklyRecurrent schedules, it is not supported to enable both settings simultaneously.  A reboot will be scheduled to occur every day at the configured time starting at the specified date and time. Setting a null (empty) date will delete the existing schedule.</Description>
          <DFFormat>
            <chr />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Dynamic />
          </Scope>
          <DFTitle>DailyRecurrent</DFTitle>
          <DFType>
            <MIME />
          </DFType>
          <MSFT:AllowedValues ValueType="None">
          </MSFT:AllowedValues>
        </DFProperties>
      </Node>
      <Node>
        <NodeName>WeeklyRecurrent</NodeName>
        <DFProperties>
          <AccessType>
            <Add />
            <Delete />
            <Get />
            <Replace />
          </AccessType>
          <Description>Value in ISO8601 date and time format (such as 2025-10-07T10:35:00) is required.  While it is supported to set either DailyRecurrent or WeeklyRecurrent schedules, it is not supported to enable both settings simultaneously.  A reboot will be scheduled to occur every week at the configured day and time starting at the specified date and time. Setting a null (empty) date will delete the existing schedule.</Description>
          <DFFormat>
            <chr />
          </DFFormat>
          <Occurrence>
            <One />
          </Occurrence>
          <Scope>
            <Dynamic />
          </Scope>
          <DFTitle>WeeklyRecurrent</DFTitle>
          <DFType>
            <MIME />
          </DFType>
          <MSFT:Applicability>
            <MSFT:OsBuildVersion>10.0.26100</MSFT:OsBuildVersion>
            <MSFT:CspVersion>1.0</MSFT:CspVersion>
          </MSFT:Applicability>
          <MSFT:AllowedValues ValueType="None">
          </MSFT:AllowedValues>
        </DFProperties>
      </Node>
    </Node>
  </Node>
</MgmtTree>
```

## Related articles

[Reboot configuration service provider reference](reboot-csp.md)
