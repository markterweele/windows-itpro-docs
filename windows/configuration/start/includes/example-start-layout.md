---
author: paolomatarazzo
ms.author: paoloma
ms.date: 03/13/2024
ms.topic: include
---

::: zone pivot="windows-10"

```xml
<LayoutModificationTemplate xmlns:defaultlayout="http://schemas.microsoft.com/Start/2014/FullDefaultLayout" xmlns:start="http://schemas.microsoft.com/Start/2014/StartLayout" Version="1" xmlns="http://schemas.microsoft.com/Start/2014/LayoutModification">
  <LayoutOptions StartTileGroupCellWidth="6" />
  <DefaultLayoutOverride>
    <StartLayoutCollection>
      <defaultlayout:StartLayout GroupCellWidth="6">
        <start:Group Name="">
          <start:DesktopApplicationTile Size="2x2" Column="0" Row="2" DesktopApplicationLinkPath="%APPDATA%\Microsoft\Windows\Start Menu\Programs\Windows PowerShell\Windows PowerShell.lnk" />
          <start:DesktopApplicationTile Size="2x2" Column="2" Row="4" DesktopApplicationLinkPath="%ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs\Accessories\Quick Assist.lnk" />
          <start:DesktopApplicationTile Size="2x2" Column="4" Row="2" DesktopApplicationLinkPath="%ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs\Accessories\Paint.lnk" />
          <start:DesktopApplicationTile Size="2x2" Column="4" Row="0" DesktopApplicationLinkPath="%APPDATA%\Microsoft\Windows\Start Menu\Programs\System Tools\File Explorer.lnk" />
          <start:DesktopApplicationTile Size="2x2" Column="0" Row="0" DesktopApplicationLinkPath="%ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs\Microsoft Edge.lnk" />
          <start:Tile Size="2x2" Column="4" Row="4" AppUserModelID="Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe!App" />
          <start:Tile Size="2x2" Column="2" Row="2" AppUserModelID="Microsoft.WindowsTerminal_8wekyb3d8bbwe!App" />
          <start:Tile Size="2x2" Column="0" Row="4" AppUserModelID="Microsoft.Windows.Photos_8wekyb3d8bbwe!App" />
          <start:Tile Size="2x2" Column="0" Row="6" AppUserModelID="Microsoft.Windows.SecHealthUI_cw5n1h2txyewy!SecHealthUI" />
          <start:Tile Size="2x2" Column="2" Row="6" AppUserModelID="Microsoft.OutlookforWindows_8wekyb3d8bbwe!Microsoft.OutlookforWindows" />
          <start:Tile Size="2x2" Column="2" Row="0" AppUserModelID="windows.immersivecontrolpanel_cw5n1h2txyewy!microsoft.windows.immersivecontrolpanel" />
        </start:Group>
      </defaultlayout:StartLayout>
    </StartLayoutCollection>
  </DefaultLayoutOverride>
</LayoutModificationTemplate>
```

::: zone-end

::: zone pivot="windows-11"

```json
{
    "pinnedList": [
        { "desktopAppLink": "%ALLUSERSPROFILE%\\Microsoft\\Windows\\Start Menu\\Programs\\Microsoft Edge.lnk" },
        { "packagedAppId": "windows.immersivecontrolpanel_cw5n1h2txyewy!microsoft.windows.immersivecontrolpanel" },
        { "desktopAppLink": "%APPDATA%\\Microsoft\\Windows\\Start Menu\\Programs\\File Explorer.lnk" },
        { "desktopAppLink": "%APPDATA%\\Microsoft\\Windows\\Start Menu\\Programs\\Windows PowerShell\\Windows PowerShell.lnk" },
        { "packagedAppId": "Microsoft.WindowsTerminal_8wekyb3d8bbwe!App" },
        { "packagedAppId": "Microsoft.Paint_8wekyb3d8bbwe!App" },
        { "packagedAppId": "Microsoft.Windows.Photos_8wekyb3d8bbwe!App" },
        { "packagedAppId": "MicrosoftCorporationII.QuickAssist_8wekyb3d8bbwe!App" },
        { "packagedAppId": "Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe!App" },
        { "packagedAppId": "Microsoft.SecHealthUI_8wekyb3d8bbwe!SecHealthUI" },
        { "packagedAppId": "Microsoft.OutlookForWindows_8wekyb3d8bbwe!Microsoft.OutlookforWindows"},
        {"secondaryTile": { "tileId": "MSEdge._pin_mjalfbhoimpkfjlpajnjkpknoe", "arguments": " --pin-url=https://www.contoso.com --profile-directory=Default --launch-tile", "displayName": "Contoso intranet", "packagedAppId": "Microsoft.MicrosoftEdge.Stable_8wekyb3d8bbwe!App", "smallIconPath": "ms-appdata:///local/Pins/MSEdge._pin_mjalfbhoimpkfjlpajnjkpknoe/ContosoLogo.png", "smallIcon": "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", "largeIconPath": "ms-appdata:///local/Pins/MSEdge._pin_mjalfbhoimpkfjlpajnjkpknoe/ContosoLogo.png" }}
    ]
}
```

::: zone-end
