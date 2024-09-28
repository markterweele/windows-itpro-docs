---
author: mestew
ms.author: mstewart
manager: aaroncz
ms.subservice: itpro-updates
ms.service: windows-client
ms.topic: include
ms.date: 10/01/2024
ms.localizationpriority: medium
---
<!--This file is shared by update/wufb-compliancedeadlines.md, /update/waas-wufb-csp-mdm.md, /update/waas-wufb-group-policy.md, and  ?/update/waas-restart.md? articles. Headings are driven by article context. Updated with 9091858 -->

These deadline policies also offer an option to opt out of automatic restarts until a deadline is reached by presenting an "engaged restart experience" until the deadline has actually expired. At that point, the device automatically schedules a restart regardless of active hours.

These notifications are what the user sees depending on the settings you choose, and what operating system version their device is running. Generally, the user notifications become more noticeable as the deadline approaches.

# [Windows 11, version 23H2 and later](#tab/23h2)

When **Specify deadlines for automatic updates and restarts** is set for Windows 11, version 23H2 and later:

While restart is pending, before the deadline occurs, users receive a toast notification in the corner of their screen. 

- If the user has set **Settings** > **Windows Update** > **Advanced options** > **Notify me when a restart is required to finish updating** to **On**, they immediately receive a toast notification when the device enters a reboot pending state for updates. 
- If the user has **Notify me when a restart is required to finish updating** set to **Off** (default), they receive a toast notification that a restart is required 24 hours after the the device enters a reboot pending state for updates.
  :::image type="content" source="./media/9091858-initial-toast.png" alt-text="Screenshot of the initial toast notification that's displayed for a user when a restart it needed for an update." lightbox="./media/9091858-initial-toast.pngg":::

- **While restart is pending, before the deadline occurs:**
   - For the first few days, the user receives a toast notification in the corner of their screen.

# [Windows 11, version 22H2 and earlier](#tab/22h2)

When **Specify deadlines for automatic updates and restarts** is set while restart is pending, before the deadline occurs:

- For the first few days, the user receives a toast notification
  :::image type="content" source="./media/9091858-initial-toast.png" alt-text="Screenshot of the initial toast notification that's displayed for a user when a restart it needed for an update." lightbox="./media/9091858-initial-toast.pngg":::

---



<!--old---

When **Specify deadlines for automatic updates and restarts** is set (For Windows 10, version 1709 and later):

 - **While restart is pending, before the deadline occurs:**

   - For the first few days, the user receives a toast notification

   - After this period, the user receives this dialog:

     ![The notification users get for an impending restart prior to deadline.](images/wufb-update-deadline-warning.png)

   - If the user scheduled a restart, or if an auto restart is scheduled, 15 minutes before the scheduled time the user receives this notification that the restart is about to occur:

     ![The notification users get for an impending restart 15 minutes prior to restart.](images/wufb-restart-imminent-warning.png)

 - **If the restart is still pending after the deadline passes:**
 
   - Within 12 hours before the deadline passes, the user receives this notification that the deadline is approaching:

     ![The notification users get for an approaching restart deadline.](images/wufb-pastdeadline-restart-warning.png)

   - Once the deadline has passed, the user is forced to restart to keep their devices in compliance and receives this notification:

     ![The notification users get for an imminent restart after the deadline.](images/wufb-pastdeadline-restartnow.png)

-->
